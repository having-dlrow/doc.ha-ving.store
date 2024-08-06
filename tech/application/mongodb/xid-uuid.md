# XID, UUID 차

UUID (Universally Unique Identifier)

```
550e8400-e29b-41d4-a716-446655440000
```

**특징**:

* 128비트(16바이트) 길이
* 네트워크 상에서 거의 고유하다는 보장을 제공
* 여러 가지 버전 (v1, v3, v4, v5) 제공

XID

```
9m4e2mr0ui3e8a215n4g
```

**특징**:

* 96비트(12바이트) 길이
* UUID보다 짧고, URL 및 파일 시스템에 적합한 문자열
* 타임스탬프, 머신 ID, PID, 카운터 기반으로 구성되어 있어 시간 순서대로 정렬 가능
* 생성 속도가 빠름

<table><thead><tr><th width="118"></th><th>UUID</th><th>XID</th></tr></thead><tbody><tr><td>길이</td><td>128비트 (16바이트)</td><td>96비트 (12바이트)</td></tr><tr><td>형</td><td>8-4-4-4-12</td><td>20자리</td></tr><tr><td>사용 사례</td><td>데이터베이스 키, 분산 시스템 식별자</td><td>데이터베이스 키, URL, 파일 시스템</td></tr></tbody></table>
