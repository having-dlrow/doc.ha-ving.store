# Git

## .gitconfig

```bash
[core]
        autocrlf = input
[user]
        name =  { username }
        email = { password }
[diff]
        tool = diffmerge
[difftool "diffmerge"]
        cmd = 'C:/Program Files/SourceGear/Common/DiffMerge/sgdm.exe' \"$LOCAL\" \"$REMOTE\"
[merge]
        tool = diffmerge
[mergetool "diffmerge"]
        trustExitCode = true
        keepBackup = false
        cmd = 'C:/Program Files/SourceGear/Common/DiffMerge/sgdm.exe' -merge -result=\"$MERGED\" \"$LOCAL\" \"$BASE\" \"$REMOTE\"
```



## Command

### Git clone

<table><thead><tr><th width="192"></th><th></th></tr></thead><tbody><tr><td>shallow clone</td><td><pre><code>git clone https://github.com/kubernetes/kubernetes -b v1.25.0 --depth 1
</code></pre></td></tr><tr><td>파일 제거 </td><td><pre><code>git clone --filter=blob:none https://github.com/kubernetes/kubernetes 
</code></pre></td></tr><tr><td></td><td></td></tr></tbody></table>

### Git

<table><thead><tr><th width="193"></th><th>command</th></tr></thead><tbody><tr><td>체크아웃 하지 않고, <br>브랜치 로컬에 가져오기</td><td><pre><code>git fetch origin &#x3C;branch_name>:&#x3C;branch_name>
</code></pre></td></tr><tr><td>체크아웃 하지 않고, <br>브랜치 삭제하기</td><td><pre><code>git push origin :&#x3C;branch_name>
</code></pre></td></tr><tr><td>merge 되돌리기</td><td><pre><code>git revert &#x3C;commit id> -m 1
</code></pre></td></tr><tr><td>git 로그 확인</td><td><pre><code>git log {branch_name} --not --remotes
git log --name-only
</code></pre></td></tr><tr><td>git commit  확인</td><td><pre><code>git branch -r --contains
</code></pre></td></tr><tr><td>작업 목록 확인</td><td><pre><code>git diff --name-status origin/{브랜치} {브랜치}
git log --name-status --author=ysyoo --oneline {commit1} {commit2} --since="2019-07-16"
</code></pre></td></tr><tr><td>브랜치 차이 확인</td><td><pre><code>git diff --name-status {commit1} {commit2} 
git diff {브랜치} {브랜치} --name-only
</code></pre></td></tr><tr><td>파일 차이 확인</td><td><pre><code>git diff HEAD {file_path}
git diff master {브랜치} -- {file_path}
git diff master -- {file_path}
git log --oneline --graph --decorate --abbrev-commit branch1..branch2
</code></pre></td></tr><tr><td>파일 되돌리기</td><td><pre><code>git checkout $(git rev-list -n 1 HEAD -- "filename")~1 -- "filename"
</code></pre></td></tr><tr><td>브랜치 Merge 여부</td><td><pre><code>git branch -r --list -a --merged {브랜치}
</code></pre></td></tr><tr><td>로그 보기</td><td><pre><code>git show --pretty="" --name-only {commit}
</code></pre></td></tr></tbody></table>

