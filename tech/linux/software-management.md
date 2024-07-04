# Software Management

## Process 목록

```
ps -eo ppid,pid,state,user,start_time,lstart,etime,cmd --sort=etime
```



## Cache Memory&#x20;

```
#sync && echo 3 > /proc/sys/vm/drop_caches
```

{% embed url="https://blog.lael.be/post/1090" %}

## Fs

```
// fs.nr_open 파라미터는 하나의 프로세스가 열 수 있는 최대 파일 개수
[root@uxe0886 home]# cat /proc/sys/fs/file-nr
193248  0       1030784
현재 오픈 가능한 최대 파일 개수 : 193248
커널에서 현재 사용중인 파일 수: 0
커널에서 최대로 오픈할 수 있는 파일 수 : 1030784

[root@uxe0886 home]# lsof | wc -l
347897
[root@uxe0886 home]# lsof -u 99 | wc -l
105298

// 현재 시스템에서 오픈되어 있는 파일의 개수
[root@uxe0886 home]# ulimit -a | grep open
open files                      (-n) 4096
```



## Port Check

```
ngrep -Wbyline port 53 and src {서버 ip}
```

```
// port 확인
yum -y install net-tools
netstat -nltp

#netstat -nap (열려 있는 모든 포트)
#netstat -nap | grep LISTEN (LISTEN 되는 모든 포트)
#netstat -nap | grep ESTABLISHED | wc -l ( 모든 서비스 동시 접속자 수)
#netstat -nap | grep :80 | grep ESTABLISHED | wc -l ( 웹 동시 접속자 수)
```

