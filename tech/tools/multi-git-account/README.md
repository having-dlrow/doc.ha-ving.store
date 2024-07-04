# - Multi Git Account

## 목적&#x20;

회사계정과 개인계정을 따로 사용

## Credential 관리

### .gitconfig 방법

```
# ~/.gitconfig
[includeIf "gitdir:~/Documents/Github/ha-ving/"]
        path = ~/.gitconfig-having.dlrow
[includeIf "gitdir:~/Documents/Github/mywork/"]
        path = ~/.gitconfig-mywork
```

```
# ~/.gitconfig-having.dlrow
[user]
 email = having.dlrow@gmail.com
 name = having.dlrow
[github]
 user = having.dlrow
```

#### workspace 만들기

```
mkdir -p ~/Documetns/Github/ha-ving/{repository_name}
git init
git add .
git commit -m "init"
```

### SSH 방법

#### 1 .ssh/config 작성

```
#personal account
Host github.com-personal
	HostName github.com
	User git
	IdentityFile ~/.ssh/id_rsa_personal

#company account
Host github.com-company
	HostName github.com
	User git
	IdentityFile ~/.ssh/id_rsa_company

# git command
# git remote add origin git@github.com-personal:personal/repository_name.git
```

## Commit Hook 만들기

```
vi .git/hooks/pre-commit.sh
```
