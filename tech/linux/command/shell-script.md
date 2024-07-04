# Shell Script

## 특수 문자

<table data-header-hidden><thead><tr><th width="128"></th><th></th></tr></thead><tbody><tr><td>특수 문자 </td><td> 사전 정의</td></tr><tr><td> ~</td><td> 홈 디렉토리</td></tr><tr><td> .</td><td> 현재 디렉토리 </td></tr><tr><td> ..</td><td> 상위 디렉토리</td></tr><tr><td> #</td><td> 주석</td></tr><tr><td> $</td><td> 쉘 변수</td></tr><tr><td> &#x26;</td><td> 백그라운드(Background) 작업</td></tr><tr><td> *</td><td> 문자열 와일드 카드(Wildcard)</td></tr><tr><td> ?</td><td> 한 문자 와일드 카드</td></tr><tr><td> []</td><td> 문자의 범위를 지정</td></tr><tr><td> ;</td><td> 쉘 명령 구분자</td></tr><tr><td> |</td><td> 파이프</td></tr><tr><td> &#x3C;</td><td> 입력 재지정</td></tr><tr><td> ></td><td> 출력 재지정</td></tr><tr><td> >></td><td> 출력 재지정 (이어 쓰기)</td></tr><tr><td> &#x26;&#x26;</td><td> 이전 명령이 정상 종료인 0의 값을 반환할 경우에만 다음 명령 실행</td></tr><tr><td> ||</td><td> 이전 명령이 비정상 종료인 1의 값을 반환할 경우에만 다음 명령 실행</td></tr></tbody></table>

\


## 명령어 파이프라

* `;` 앞의 명령어가 실패해도 다음 명령어가 실행
* `&&` 앞의 명령어가 성공했을때 다음 명령어가 실행 ✔
* `&` 앞의 명령어를 백그라운드로 돌리고 동시에 뒤의 명령어를 실행



<details>

<summary>For</summary>

```
time for i in {1..10}; do sleep 1; done
real    0m10.052s
user    0m0.005s
sys 0m0.018s
```

</details>

<details>

<summary>Multi Line</summary>

```
cat > test <<EOF
test from yeonsoo
this make write multiple line
EOF
```

</details>
