---
description: '#_컨테이너_실전_구축_및_배포 방안'
---

# Cron

## 실행

```
FROM ubuntu:16.04

RUN apt update
RUN apt install -y cron 

COPY task.sh /usr/local/bin
COPY cron-example /etc/cron.d
RUN chmod 0644 /etc/cron.d/cron-example

CMD["cron", "-f"]
```

백그라운드 프로세스이므로, CMD를 사용하여 `cron -f`  foreground로 실행 되도록 한다.

```
docker image build -t example/cronjob:latest .
docker container run -d --rm --name cronjob example/cronjob:latest
docker container exec -it cronjob tail -f /var/log/cron.log
```



## 비정상적 종료

외부에서 docker stop 명령 등으로 SIGTERM 신호를 보내 컨테이너를 종료한다.



컨테이너 종료를 막기 위해  `tail -f /dev/null` 을 실행하는 방법이 있다. tail 명령이 SIGTERM 으로는 종료되지 않는다. 떄문에 docker container stop 명령 후 timout이 지나도 컨테이너가 완전히 종료되지 않는 문제가 있다. 대체하여 `sleep infinity` 사용하자.
