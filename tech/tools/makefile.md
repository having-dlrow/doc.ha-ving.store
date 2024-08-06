# Makefile

## 변수 선언

```
TEMP ?= /temp        # 선언되어 있지 않으면 TEMP(/temp) #ifdef 동일
```

```
TEMP = $(CC)/temp     # CC가 어디에 있든, TEMP(test/temp)
CC = test
```

```bash
TEMP := $(CC)/temp    # CC가 없으면 TEMP(/temp)
CC = test
TEMP := $(CC)/temp    # CC가 있으면 TEMP(test/temp)
```



## 자동 변수

```
$@    // 파일명이 `foo.a(bar.o)` 일때, `foo.a`
$*    // (확장자 없는) 파일명
$%    // 파일명이 `foo.a(bar.o)` 일때, `bar.o`
$<    // 예를 들어 `all:library.cpp main.cpp` 이면, $@ 'all', $< 'library.cpp', $^ 전체
$^    // 전체
$?    // 현재의 Target 파일의 최근 갱신된 파일명
```



## Phony

* Makefile에게 해당 타겟이 실제 파일이 아닌 명령어를 실행하기 위한 것임을 알려준다.\
  이를 통해 파일 이름과 타겟 이름이 충돌할 경우 발생할 수 있는 문제를 방지한다.

1. 파일 이름과 타겟 이름 충돌 방지
   1. `clean` 파일이 존재하는 경우
      1. `make clean` 명령어 실행 > 파일 타임스탬프 확인 > 최신 상태 간주 > 명령어 실행 안함
   2. .PHONY 사용시
      1. 항상 실행해야 하는 명령어임을 인식 > 파일 존재여부와 상관없이 명령어 실행
2. 명확한 의도 표시&#x20;
   1. .PHONY을 사용하여, 파일과 관련된 것이 아닌, 빌드 작업임을 명확히 한다.

Example 1

```
.PHONY: clean
clean:
    rm temp
```

* clean 이라는 타겟은 항상 실행된다.
* temp 라는 파일이 존재하더라도 Make 실행은 파일 여부와 관련되지 않음으로 인식

```
clean:
    rm temp
```

* temp 파일이 존재하고, 최신 상태로 간주되면
  * \`make clean\` 실행 안됨
