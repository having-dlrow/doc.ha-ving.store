---
description: https://livebook.manning.com/book/microservices-patterns/chapter-4/110
---

# ✔️ SAGA Pattern

## N Phase Commit

* **2 Phase Commit** ( = Protocol )
  * "다수 노드 데이터베이스에서 커밋을 구현하는 개념으로 시작"
  * 약속된 규약, Protocol 방식
  * 2PC 구현을 위해 **Cordinator(인프라)가 필요**

```
[Prepare]
1. Coordinator가 Global Unique ID 생성
2. 참여자들에게 준비 요청

[Commit Start]
3. (참여자)준비 완료했어 (or 실패했어) -> (Coordinator)
[Commit Done
4. (Coordinator) 준비가 하나 실패  -> Abort -> (참여자)
   (Coordinator) 준비전체 완료     -> Commit -> (참여자)
```

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

:warning: **Coordinator 문제가 생기더라도, 비지니스 문제를 최소화 해야한다.**

:warning: **데이터 Lock 으로 인한 가용성 한계**

## 보상 트랜젝션 ( Compensating Transaction )

* 일련의 작업을 보상(보정) 하기 위한 트랜잭션 구현
* "Commit" 된 데이터를 Undo 하기 위한 작업

:warning:  이슈 발생에 대해 롤백하는 개념, **이슈 발생 상황에서 복구 처리가 가능한 로직이어야 함**

## SAGA (2PC + 보상 트랜잭션)

* 트랜잭션 관리 주체 : Application 단위
* ACID
  * 작업이 실패하면 이전까지 작업된 마이크로 서비스에 <mark style="color:blue;background-color:blue;">보상 이벤트를 소싱하여,</mark> <mark style="background-color:blue;">**원자성 보장**</mark>
    * 보상 트랜잭션
  * **데이터 정합성**
* 2PC ( 2 Phase Commit ) 같은 방식을 사용 할 수 없고, 이벤트 / 명령어 방식으로 한다.

<figure><img src="../../../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

### Chreography 패턴

* Orchestrator 을 두지 않고 Saga 구현
  * 구현은 간편하지만, **트랜잭션 모니터링 어렵다.**

### Orchestration 패턴

* **Orchestrator 두어**, Saga(Transaction) 관리

<figure><img src="../../../../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

