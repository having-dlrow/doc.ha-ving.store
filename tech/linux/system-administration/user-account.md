# User Account

## Local User Account

<table><thead><tr><th width="152"></th><th></th></tr></thead><tbody><tr><td>create</td><td><pre><code>sudo useradd -m {username} -s /bin/bash -c {comment}
</code></pre></td></tr><tr><td>password</td><td><pre><code>sudo passwd {username}
</code></pre></td></tr><tr><td>update</td><td><pre><code>sudo usermod -s /bin/tcsh
</code></pre></td></tr><tr><td>show</td><td><pre><code>id
</code></pre></td></tr><tr><td>add group</td><td><pre><code>sudo usermod -g {group_name} {username}
sudo usermod -a -G {group_name} {username} 
// -a ( additional )
// -G ( 보조 그룹 )
</code></pre></td></tr><tr><td></td><td></td></tr></tbody></table>



### /etc/passwd

&#x20; <mark style="color:red;">모든 계정에 대한 정보를 답고 있는 설정 파일</mark>&#x20;

```
{username}:x:1002:1002:{comment}:/home/{username}:/bin/bash
```

### /etc/group

```
{group_name}:x:1003:
```

### /etc/shadow

&#x20; 로그인  username : password&#x20;

### <mark style="color:blue;">/etc/security/limits.conf</mark> ( ulimit )

* /etc/security/limits.d/{username}.conf  : 개인 별 설정 파일&#x20;
* User의 리소스 제한 값

### pam\_limits

* `*` :   wildcard ,&#x20;
* `%` : group wildcard
* hard : kernel에 의해 제한 받음
* soft : 허용 범위 내에서 제한 (기본값)
* core :&#x20;

```
#<domain>     <type>     <item>     <value>
#

*             soft         core          0
root          hard         core          100000
*             hard         rss           10000
@student      hard         nproc         20
@faculty      soft         nproc         20
@faculty      hard         nproc         50
ftp           hard         nproc         0
```
