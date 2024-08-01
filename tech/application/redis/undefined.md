# 4. 임계점

## CPU

* Redis는 Single Thread 구성으로, 하나의 CPU 코어를 사용한다.\
  (서버가 멀티 코어이더라도)
* 따라서, 단일 성능이 높은 4코어 장치가 32코어보다 빠른 성능을 갖는다.

## Memory

<details>

<summary><span data-gb-custom-inline data-tag="emoji" data-code="26a0">⚠️</span> swap 구성하자</summary>

* 64비트 환경에서 제약이 없음 ( swap 메모리 까지 사용 )
  * 에러 발생, 꼭 제약을 넣을 것!
* 32비트 환경에서 최대 3G 메모리 사용
* swap 사용 안하면,&#x20;
  * maxmemory-policy 설정값에 따라 에러발생 혹은 데이터 삭제 조치
* swap 사용,
  * maxmemory 설정 이상 사용시, 디스크를 가상 메모리 공간으로 사용

</details>

### Max Memory

* 4G 이내로 설정하자
* rdb 설정을 사용한다면,  `메모리 = 2 * max-memory + 관리 메모리`

<details>

<summary><span data-gb-custom-inline data-tag="emoji" data-code="26a1">⚡</span>그림 같이 Copy On Write 최대 데이터 발생 시나리오</summary>

1. BGSAVE
2. SAVE 60 10000
3. 신규 slave 연결로 인해, Full Sync
4. auto-aof-rewrite-percentage 100  # Aof fork 100% 커지면 다시 쓰기
5. bgrewrite AOF

5개의 상황, 즉 fork 함수 실행으로 자식 프로세스가 동작 될 때, \
모든 메모리가 변경이 발생하게 된다면 최대 2배를 사용하게 된다.

:warning: <mark style="color:blue;">로그에 COW 값이 남으니 꼭! 모니터링이 필요하다.</mark>

</details>

<figure><img src="../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

* <mark style="color:red;">aof, rdb을 사용한다면,  swap 사이즈를 4G 설정하자</mark>

<div align="left">

<figure><img src="../../../.gitbook/assets/Untitled (2).png" alt="" width="375"><figcaption></figcaption></figure>

</div>

