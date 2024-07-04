# Process

* **Process**: 독립적인 실행 단위, 독립된 메모리 공간과 자원을 소유.
* **Thread**: 프로세스 내 실행 단위, 같은 프로세스 내에서 메모리를 공유하며 병렬 처리를 가능하게 함.
* **Procedure**: 프로그램 내에서 특정 작업을 수행하는 코드의 일련의 단계, 함수 또는 서브루틴으로도 불림.



## 프로그램

실행 파일 형태로 `.exe`, `,py` 등파일들의 집합

## 프로세스

### 1.프로그램  로드

프로그램이 실행 하면, 프로그램이 메모리에 로딩된다.

### 2.프로세스 생성

OS는 프로그램 실행을 위해 메모리, CPU, 파일 같은 자원의 정보와 프로세스 정보를 Process Control Block에 생성한다.



#### 좀비 프로세스

* 자식 프로세스가 종료되었지만, 부모 프로세스가 종료 상태를 읽지 않아, PCB에 정보가 남아 있는 상태이다
* 할당된 자원(CPU, 메모리) 등이 해제되었고, PCB에 정보가 남아 있는 상태이다.
* 이후, 부모 프로세스가 `wait()` `waitpid()` 시스템 호출을 통해 종료 상태를 확인하여 PCB에서 제거 될수 있다.

#### 고아 프로세스

* 자식 프로세스가 동작하고 있는데, 부모 프로세스가 없는 상태이다.
* 이런 경우, PID 1 프로세스에 입양된다.



### 3.  프로세스 관리

<table><thead><tr><th width="120">이름</th><th width="59">번호</th><th>의미</th><th></th></tr></thead><tbody><tr><td>HUP</td><td>1</td><td> Hangup</td><td>실행 종료, 접속이 끊어짐을 의미</td></tr><tr><td>INT</td><td>2</td><td>Interrupt</td><td>실행 종료 ( CTRL + C )</td></tr><tr><td>QUIT</td><td>3</td><td>Quit</td><td>실행 종료 ( CTRL  + \ )</td></tr><tr><td>KILL</td><td>9</td><td>Kill</td><td>무조건 종료</td></tr><tr><td>SEGV</td><td>11</td><td>Segmentation Violation</td><td>허가되지 않은 메모리 은 메모리영역에 접근하였다.</td></tr><tr><td>TERM</td><td>15</td><td>Termination</td><td>최대한 정상 종료</td></tr><tr><td>STOP</td><td>19</td><td></td><td>무조건 즉각 정지</td></tr><tr><td>TSTP</td><td>20</td><td></td><td>실행을 정지 후 다시 실행을 계속하기 위하여 대기</td></tr><tr><td>CONT</td><td>18</td><td>Continue</td><td>Stop 이나 Tstop에 의해 정지된 프로세스가 다시 실행을 지속</td></tr></tbody></table>

4. 명령어
   1. 프로세스  확인 방법  uptime, top, w
   2. 프로세스 우선순위 부여 방법 : nice
