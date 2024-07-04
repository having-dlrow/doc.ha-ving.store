# CascadeType

## 개념

1. 부모 엔티티가 삭제될 때 자식 엔티티도 삭제
2. 특정 엔티티를 영속 상태로 만들 때 연관된 엔티티도 함께 영속 상태로 전이

## 종류

<table><thead><tr><th width="224"></th><th></th></tr></thead><tbody><tr><td>CascadeType.ALL</td><td>모든 Cascade 적용</td></tr><tr><td>CascadeType.PERSIST</td><td>연관된 하위 엔티티도 함께 유지한다.</td></tr><tr><td>CascadeType.REFRESH</td><td>연관된 하위 엔티티도 모두 새로고침한다.</td></tr><tr><td>CascadeType.MERGE</td><td>엔티티 상태를 병합(Merge)할 때, 연관된 하위 엔티티도 모두 병합</td></tr><tr><td>CascadeType.REMOVE</td><td>엔티티를 제거할 때, 연관된 하위 엔티티도 모두 제거한다.</td></tr><tr><td>CascadeType.DETACH</td><td>부모 엔티티를 detach() 수행하면, 연관 하위 엔티티도 detach()상태가 되어 변경 사항을 반영하지 않는다.</td></tr></tbody></table>

## 고려사항

### <mark style="color:blue;">CasecadeType.Remove</mark>

1. 부모 엔티티가 삭제 > 자식 엔티티도 삭제.
2. <mark style="color:blue;">부모 엔티티가 자식 엔티티와의 관계를 제거 >  자식 엔티티는 삭제되지 않고 그대로 남아있다.</mark>

### orphanRemoval ( 보완재 )

1. 부모 엔티티가 삭제되면 자식 엔티티도 삭제 된다.&#x20;
2. 그런데 CasecadeType.Remove와는 달리,
3. 부모 엔티티가 자식 엔티티와의 관계를 제거 > <mark style="color:blue;">자식은 고아로 취급되어 그대로 사라진다.</mark>
4. <mark style="color:blue;">기본값은 false (삭제안함) 이다.</mark>
