# 🧜‍♂️ 운영체제

### 출처

[이화여자대학교 OS 강의 - 반효경 교수님](https://core.ewha.ac.kr/publicview/C0101020140307151724641842?vmode=f)



## 1. OS introduction

#### 운영체제(Operating System, OS)란?

컴퓨터 하드웨어 바로 위에 설치되어 사용자 및 다른 모든 소프트웨어와 하드웨어를 연결하는 소프트웨어 계층

- 협의의 운영체제(커널) - 운영체제의 핵심 부분으로 메모리에 상주하는 부분

- 광의의 운영체제 - 커널 뿐 아니라 각종 주변 시스템 유틸리티를 포함한 개념

![운영체제란](https://user-images.githubusercontent.com/58287684/100165123-c82d9980-2efc-11eb-8c23-2fa1559a65dd.png)



#### 운영체제의 목적

컴퓨터 시스템의 **자원을 효율적**으로 관리

사용자가 컴퓨터 시스템을 **편리하게 사용**할 수 있는 환경을 제공



#### 운영체제의 분류

1. 동시작업 가능 여부
   - 단일작업 - 한 번에 하나의 작업만 처리 ex) MS-DOS
   - 다중작업 - 동시에 두 개 이상의 작업 처리 ex) UNIX, Windows

2. 사용자의 수
   - 단일 사용자 ex) MS-DOS, Windows
   - 다중 사용자 ex) UNIX, NT server
3. 처리방식
   - 일괄처리 (batch processing)
     - 한꺼번에 모아서 처리
   - 시분할 (time sharing)
     - 여러 작업을 수행할 때 일정한 시간단위로 분할하여 사용
     - 일괄처리에 비해 짧은 응답시간을 가짐
   - 실시간(Realtime OS)
     - 정해진 시간안에 어떠한 일이 반드시 종료됨이 보장되어야하는 실시간시스템을 위한 OS
     - ex) 원자로/공장제어, 미사일 제어, 반도체 장비, 로보트 제어 등



#### 몇 가지 용어 정리

- `Multitasking`  : 한 컴퓨터에서 여러 작업을 동시의 수행, cpu가 빠르게 돌면서 각각의 task를 번갈아가며 일을 수행 -> 행위 강조
- `Multiprogramming` : 메모리에 여러 프로그램이 동시에 올라간것 -> 메모리 측면을 강조
- `Time sharing` : CPU의 시간을 분할하여 수행 -> 나누어 쓴다는 의미를 강조
- `Multiprocess` : 여러 프로그램이 동시에 수행
- `Multiprocessor` : 하나의 컴퓨터에 여러개의 CPU(processor)가 붙어있음을 의미



#### 운영체제의 구조

- CPU 관리
- 메모리 관리
- 파일 관리
- 입출력 관리 - 인터럽트로 CPU에게 요청함
- 프로세스 관리

![컴퓨터시스템구조](https://user-images.githubusercontent.com/58287684/100165035-8e5c9300-2efc-11eb-814c-4c9d318ef20e.png)





## 2. System Structure & Program Execution

#### 컴퓨터 시스템 구조

![운영체제 기능](https://user-images.githubusercontent.com/58287684/100165080-acc28e80-2efc-11eb-839f-5b41425d0330.png)

- `CPU` : 인스트럭션만 실행하는것이 CPU의 숙명. 메모리 몇번지에 있는 일을 하라 라는 것이 적혀있음
- `timer` : 특정 프로그램이 CPU를 독점하는 것을 막기 위해 만료시간을 정해둔다. 할당 시간이 초과한다면 인터럽트를 발생시켜 CPU에게 알려준다.
  - 정해진 시간이 흐른 뒤 운영체제에게 제어권이 넘어가도록 인터럽트 발생
  - 타이머는 매 클럭 틱 때마다 1씩 감소
  - 타이머 값이 0이 되면 타이머 인터럽트 발생
  - CPU를 특정 프로그램이 독점하는 것으로부터 보호
  - 타이머는 time sharging을 구현하기 위해 널리 이용되고 현재 시간을 계산하기 위해 사용되기도 함

- `mode bit` : CPU에서 운영체제가 가지고있느냐 사용자 프로그램이 가지고있느냐를 구분해준다.
  - 사용자 프로그램의 잘못된 수행으로 다른 프로그램이나 운영체제에 피해가 가지않도록 하기위한 보조 장치이다.
  - 1 사용자 모드 : 사용자 프로그램 수행 -> 접근에 제한이 있음 한정된 인스트럭션만!
  - 0 모니터 모드(= 커널모드, 시스템모드) : OS 코드 수행 -> 모든 것에 접근 가능
    - 보안을 해칠 수 있는 중요한 명령어는 모니터 모드에서만 수행가능한 '특권명령'으로 규정
    - Interrupt나 Exception 발생시 하드웨어가 mode bit을 0으로 바꿈
    - 사용자 프로그램에게 CPU를 넘기기 전에 mode bit을 1로 셋팅

- `Device controller` : 각 장치를 통제하는 일종의 작은 CPU -> hardware
  - I/O device controller
    - 제어 정보를 위해 controller register, status register를 가짐
    - local buffer를 가짐 (일종의 data register)
  - 입출력은 실제 device와 local buffer 사이에서 일어남
  - 입출력이 끝났을 경우 interrupt로 CPU에 그 사실을 알림
  - `Device driver` : 운영체제가 각각의 디바이스에 접근하게 하기위한 인터페이스 역할을 하는 소프트웨어

- `DMA controller` : I/O장치가 자주 인터럽트를 걸게되면 CPU가 너무 방해를 받게 되서 효율이 떨어지기 때문에 중간에서 I/O에서 걸어준 인터럽트를 메모리에 복사해주는 일을 한다.

