# Find

## awk

```
logtail /apache/logs/php_error_log | awk '{if ($0 ~ "Warning") { print $0}}'
tail -f /apache/logs/php_error_log* | grep -E '(Warning|Fatal)'
grep -rn Warning /apache/logs/php_error_log* | sort | uniq
```

## find

<details>

<summary>userid.domain.com 글자 찾기</summary>

```
// php
find /test1 /test2 -type f -name '*.php' | xargs grep -Ein --color '(userid|user_id)(.*)domain\.com'
find /test1 /test2 -type f -name '*.php' | xargs grep -Ein --color 'sprintf(.*)\%s\.domain\.com(.*)(userid|user_id)'
// tpl
find /test1 /test2 -type f -name '*.tpl'| xargs grep -Ein --color '(userid|user_id)(.*)domain\.com'
// js
find /test1 /test2 -type f -name '*.js'| xargs grep -Ein --color '(userid|user_id)(.*)domain\.com'
```

</details>

