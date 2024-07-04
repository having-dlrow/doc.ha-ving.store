# 🎮 Command

## Redis 시스템 리소스 확인

```
redis-cli --stat
```

### INFO STAT

<table><thead><tr><th width="275">설정값값</th><th>설명</th></tr></thead><tbody><tr><td><mark style="color:red;">total_connections_received</mark></td><td>서버 시작후 총 접속 수</td></tr><tr><td>total_commnads_processed</td><td>서버 시작후 총 처리한 명령 수 ( 저장.조회 모두)</td></tr><tr><td>total_net_input_bytes</td><td>서버 시작후 총 입력 바이트</td></tr><tr><td>total_net_output_bytes</td><td>서버 시작후 총 출력 바이트</td></tr><tr><td><mark style="color:red;">rejected_connections</mark></td><td>max client 제한으로 거부된 접속 수</td></tr><tr><td>expired keys</td><td>expire 명령으로 삭제된 키 수</td></tr><tr><td>evicted keys</td><td>memory 제한으로 퇴출된 키 수</td></tr><tr><td>sync_full</td><td>master node 인 경우, slave 와 sync 한 횟수</td></tr><tr><td>sync_partial_ok</td><td>err</td></tr><tr><td><mark style="color:red;">keyspace_misses</mark></td><td>노드에 조회되지 않는 키가 조회된 횟수</td></tr></tbody></table>

### Memory STAT

<table><thead><tr><th width="279">설정값</th><th>설명</th></tr></thead><tbody><tr><td><mark style="color:red;">used_memory</mark></td><td>Redis 서버에 현재 할당된(libc, jemalloc, tcmalloc 등) 메모리 크기 (byte)</td></tr><tr><td>used_memory_rss</td><td>운영체제에서 볼 때 Redis가 할당한 byte 수</td></tr><tr><td>used_memory_peak</td><td>Redis에 할당되었던 최대 메모리 크기 (byte)</td></tr><tr><td>used_memory_overthread</td><td>사용자 메모리 크기에 대한 overthread</td></tr><tr><td>used_memory_startup</td><td>최초 할당되었던 Redis 메모리 크기 (byte)</td></tr><tr><td><mark style="color:red;">used_memory_dataset</mark></td><td>사용자 데이터가 저장된 메모리 크기 (byte),<br>(used_memory - used_memory_overhead)</td></tr><tr><td>total_system_memory</td><td>현재 사용 가능한 시스템 메모리 총 크기 (byte)</td></tr><tr><td>maxmemory</td><td>Maxmemory 파라메터에 설정된 메모리 크기 (byte)</td></tr><tr><td><mark style="color:red;">maxmemory_policy</mark></td><td>Maxmemory_policy 파라메터에 설정된 메모리 크기 (byte)</td></tr><tr><td>mem_fragmentation_ratio</td><td>메모리 단편화 상태비율</td></tr><tr><td>active_defrag_running</td><td>조각 모음이 활성 상태인지 나타내는 플래그</td></tr><tr><td>used_cpu_sys</td><td>시스템 모드에서 사용한 CPU 시간(초)</td></tr><tr><td>used_cpu_user</td><td>사용자 모드에서 사용한 CPU 시간(초)</td></tr><tr><td>used_cpu_sys_children</td><td>RDB/AOF 파일 저장 시 자식 프로세스가 시스템 모드에서 사용한 CPU 시간(초)</td></tr><tr><td>used_cpu_user_children</td><td>RDB/AOF 파일 저장 시 자식 프로세스가 사용자 모드에서 사용한 CPU 시간(초)</td></tr><tr><td><mark style="color:red;">commands_processed</mark></td><td>초당 처리되는 명령어 수</td></tr><tr><td>aof_rewrite_scheduled</td><td>AOF 파일을 저장하는 스케줄 설정 1, 아니면 0</td></tr><tr><td>aof_pending_bio_fsync</td><td>i/o 부하가 심해서 현재 처리 하지 못하고 대기중인 현재의 잡(job)의 수</td></tr><tr><td>aof_pending_bio_fsync</td><td>i/o 부하가 심해서 2초 이상 쓰지 못한 경우, 서버 메시지를 남기고 이항목을 1증가 시킨다.</td></tr><tr><td>pubsub_channels</td><td>pub/sub channel로 연결된 channel 수</td></tr><tr><td>pubsub_patterns</td><td>pub/sub pattern으로 연결된 pattern channel</td></tr></tbody></table>

## Redis 데이터 사이즈  확인

```
redis-cli dbsize
redis-cli keyspace
redis-cli dbsize info # 상세
```

## Redis Client 목록  확인

```
redis-cli client list
```

## 데이터 덤프

```
redis-cli save
redis-cli --csv --scan > 2022.csv
```

## 데이터 적용

```
redis-cli --rdb {.rdb 파일 위치}
```
