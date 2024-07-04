# Apache

## Module

### List

```
httpd -l     # 현재 설정된 모듈 리스트 확인
```

### Multi Processing Module

#### ✅ Prefork

* 프로세스를 복제하여 실행
  * 따라서, 메모리 영역까지 복제하기 때문에, 메모리 사용량이 많다.
* 프로세스간 메모리 공유가 없으므로, 안정적이다.
* 기업에서 주로 사용한다

#### Worker

* 미리 만든 Worker(Child Process)가 각각의 요청을 담당.
* 동시 접속이 많은 경우 사용
* Thread 간 Lock 상황이 발생 될 수 있다.&#x20;



## Conf

<table><thead><tr><th width="147">name</th><th width="477">설명</th><th>기본값</th></tr></thead><tbody><tr><td>Max Client</td><td>동시에 접속 가능한 클라이언트의 최대 수</td><td>256</td></tr><tr><td>Server Limit</td><td>프로세스 수의 최대 수</td><td>256</td></tr></tbody></table>

※ ServerLimit >= MaxClient 로 설정



