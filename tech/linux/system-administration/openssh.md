# OpenSSH

## SSH

Root 계정 추가

```
sudo passwd root
```

SSH 서버 설치

```
sudo apt install openssh-server
```

설정 수정

```
vi /etc/hosts.allow
-------------------------------
sshd: {{ ip }} 
```

SSH 서버 활성화

```
sudo systemctl enable --now ssh
sudo systemctl restart ssh
```

GUI 부팅 끄기

```
sudo systemctl set-default multi-user.target
sudo systemctl isolate multi-user.target              // 지금 전환
```

## SCP

```
scp -r {user}@{ip}:{absolute_file_path} .
```
