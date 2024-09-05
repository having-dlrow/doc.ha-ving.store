# - 동시 편집 OT / CRDT

## <mark style="background-color:yellow;">CRDTs solve distributed data consistency challenges</mark>

[https://ably.com/blog/crdts-distributed-data-consistency-challenges#use-cases-for-crdts](https://ably.com/blog/crdts-distributed-data-consistency-challenges#use-cases-for-crdts)&#x20;

## Conflict Free Replicated Data Type

<table><thead><tr><th width="117"></th><th width="305">OT</th><th>CRDT (P2P)</th></tr></thead><tbody><tr><td>상품</td><td>Google Docs , Ms 365 online</td><td>TomTom,  GPS, </td></tr><tr><td>특징</td><td>편집시간, 인덱스 기반</td><td>Stream ID 부여(트리구조)</td></tr><tr><td>장점</td><td></td><td>중앙 서버 필요 없음</td></tr><tr><td>단점</td><td></td><td>메모리 사용 높음.  log(n) 조회</td></tr></tbody></table>



OT

<figure><img src="../../../.gitbook/assets/image (4) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* [https://github.com/Operational-Transformation/ot.js](https://github.com/Operational-Transformation/ot.js)
* [https://github.com/gulf/gulf](https://github.com/gulf/gulf)

CRDT

: data structure  제공하여, 데이터 consistency가 자동 지켜질 수 있도록 하는 컨

* [https://automerge.org/](https://automerge.org/)
* [https://docs.yjs.dev/](https://docs.yjs.dev/)



오픈소스

* &#x20;Yorkie
  * [https://www.youtube.com/watch?v=6LhMuuyAg\_E](https://www.youtube.com/watch?v=6LhMuuyAg\_E)
* Monaco
  * [https://microsoft.github.io/monaco-editor/](https://microsoft.github.io/monaco-editor/)
