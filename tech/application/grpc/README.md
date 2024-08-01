# 🎧 gRpc

## 이해하기

gRPC

* 공통 규약
* 다양한 언어/플랫폼 지원
* 높은 메시지 압축률 (성능)
* 양방향 스트리밍 처리 가능

protocol Buffer

* 장) IDL 자동생성, 데이터의 효율성이 높다
  * 정해진 자리, 정해진 타입, convert 필요 없이 바이트 그대로 사용 가능
  * 정해진 규약, 의사소통 비용 감소
* 단) 정해진 문법(IDL)을 배워야 한다.

**Server**

* `1(req):1(resp)`: Unary Call
  * onNext 1회 → onCompleted
* `N(req):1(resp)` : Server Stream
  * onNext N회 (Server) → onCompleted
* `1(req):N(resp)` : Client Stream
  * onNext N회 (Client) → onCompleted
* `N(req):M(resp)` : Bi Stream
  * onNext N회 (Server) → onNext N회(Client) → onCompleted

Client

* `channel` : socket 연결
* `stub` : channel을 통해 rpc 호출 할 수 있는 추상화된 객체
  * `blocking` : 응답 대기 ( 타임아웃 exception 발생 )
    * `newBlockingStub()`
  * `async` : 비동기 응답, ( streaming 방식에는 async 사용이 국룰? )
    * `newStub()`
  * `futer` :

Proto 형태 (IDL)

```bash
syntax = "proto3";

option java_multiple_files = true;
option java_outer_classname = "EventProto";
option java_package = "com.example.demo.proto";

package com.tistory.jeongpro.event;

message EventRequest { 
       string sourceId = 1;
       string eventId = 2; 
}

message EventResponse { 
				string result = 1; 
}

service NewdataService { 
	rpc unaryEvent(EventRequest) returns (EventResponse) {} 
	rpc serverStreamingEvent(EventRequest) returns (stream EventResponse) {} 
	rpc clientStreamingEvent(stream EventRequest) returns (EventResponse) {} 
	rpc biStreamingEvent(stream EventRequest) returns (stream EventResponse) {} 
}
```

*   Create Client

    `ManagedChannelBuilder` 사용 합니다.

    ```bash
    // 1. 새로 생성
    ManagedChannelBuilder.forAddress(host, port).usePlaintext()

    // 2. 기존 channel 사용
    ManagedChannelBuilder channelBuilder 
    channel = channelBuilder.build();
      // 2-1. blocking stub
      blockingStub = RouteGuideGrpc.newBlockingStub(channel);
      // 2-2. aysnc stub
      asyncStub = RouteGuideGrpc.newStub(channel);

    ```
*   Client-side streaming RPC Call

    ```bash
    // 응답 들을 거 연결
    StreamObserver<RouteSummary> responseObserver = new StreamObserver<RouteSummary>() {
        @Override
        public void onNext(RouteSummary summary) {

        }

        @Override
        public void onError(Throwable t) {

        }

        @Override
        public void onCompleted() {

        }
      };

    // N개 보내기
    StreamObserver<Point> requestObserver = asyncStub.recordRoute(responseObserver);
    try {
    	for( req i : requests ) {
    		requestObserver.onNext(req);
    		Thread.sleep(rand.nextInt(1000) + 500);
    	}
    } catch ( RuntimeException e ) { 
    		requestObserver.onError(e);
    }

    requestObserver.onCompleted();
    ```
*   Create Server

    ```bash
    ----Runner ---

    @PostConsturct
    server = ServerBuilder.addService(kafkaMessengerImpl).build();

    @run
    server.start();
    ```

## 설정 하기

*   intellij

    settings > plugins

    * `protobuf`
      * intellij 2021.02 버전 부터는 `grpc` , `protocol Buffers` 을 disable 처리하고, protobuf 만 사용 하면 됨.
      * syntax highlighting ( brace matching, element )
*   gradle generate Proto files

    1. src/main/proto 생성
    2. src/main/proto 에 Hello.proto 생성
    3. build.gradle

    ```bash
    // 1. generated class 가 java compile path 에 들어가도록 설정.
    sourceSets {
        main {
            java {
                srcDirs += [
                        'build/generated/source/proto/main/grpc',
                        'build/generated/source/proto/main/java'
                ]
            }
        }
    }

    // 2. generated class 가 intelliJ 인식 되도록 설정.
    protobuf {
        protoc {
            artifact = "com.google.protobuf:protoc:$proto_version"
        }
        plugins {
            grpc {
                artifact = "io.grpc:protoc-gen-grpc-java:$grpc_version"
            }
        }
        generateProtoTasks {
            all()*.plugins {
                grpc {}
            }
        }
    }
    ```

    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ab3a3ae9-cf02-41b0-aa0a-3209c45e1ff3/Untitled.png)
* ~~server/client 프로젝트에 .jar 파일 추가 하기~~

## 예제 해보기

`CountDownLatch`

*   **eventqueue**

    ```bash
    [client(consistent-manager)] —> [server][client(grpc-application)] —> [server(executer)]
    ```

    * `Client-side Streaming RPC` ( consistent-manager , grpc-application 의 구현 방식)
*   🔰 **Deadline** 또는 **timeout**

    [gRPC and Deadlines](https://grpc.io/blog/deadlines/)

    \<aside> 📌 언어에 따라 deadline 혹은 timeout 으로 명명함.

    \</aside>

    *   🙏🏻 데드라인 (onCompleted 호출까지 기다리는 시간), 긴\~숫자 여도 좋아! 꼭 설정해두세요!!

        deadline 또는 timeout에 적정한 값은 없는가? simple code 기준, 100millisecond 으로 권장.

        그렇지만, end to end (전체 시스템의) 을 고려하자, ( eg. 네트워크 latency )

        Go ( Server )

        ```bash
        clientDeadline := time.Now().Add(time.Duration(*deadlineMs) * time.Millisecond)
        ctx, cancel := context.WithDeadline(ctx, clientDeadline)
        ```

        Java ( Server )

        ```bash
        response = blockingStub.withDeadlineAfter(deadlineMs, TimeUnit.MilliSECOND)
                               .sayHello(request)
        ```
    *   Client 에서, deadline 체크 해서 biz 로직

        Go ( Client )

        ```bash
        if ctx.Err() == context.Canceled {
        	return status.New(codes.Canceled, "Client cancelled, abandoning");
        }
        ```

        Java ( Client )

        ```bash
        if ( Context.current().isCancelled()) {
        	responseObserver.onError(Status.CANCELLED.withDescription("Cancelled by client").asruntimeException());
           return;
        }
        ```
* ### 🔰 retry
* 🔰 **Network Err**
  * `14 UNAVAILABLE: TCP Read failed` :
  * `14 UNAVAILABLE: failed to connect to all addresses` :
  * `UNAVAILABLE: Connection closed after GOAWAY` : 상대 서버가 없어진 경우
*





Ref

* [http://xingyys.tech/grpc2/](http://xingyys.tech/grpc2/)
* [https://github.com/trajano/grpc-chunker-java](https://github.com/trajano/grpc-chunker-java)
* [https://christina04.hatenablog.com/entry/grpc-keepalive](https://christina04.hatenablog.com/entry/grpc-keepalive)
* [https://grpc-ecosystem.github.io/grpc-gateway/docs/mapping/customizing\_your\_gateway/](https://grpc-ecosystem.github.io/grpc-gateway/docs/mapping/customizing\_your\_gateway/)
* [https://github.com/grpc-ecosystem/go-grpc-middleware](https://github.com/grpc-ecosystem/go-grpc-middleware)
