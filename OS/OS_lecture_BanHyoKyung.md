# 🧜‍♂️ 운영체제

### 출처

[이화여자대학교 OS 강의 - 반효경 교수님](https://core.ewha.ac.kr/publicview/C0101020140307151724641842?vmode=f)



## 01. OS introduction

#### 1. 운영체제(Operating System, OS)란?

컴퓨터 하드웨어 바로 위에 설치되어 사용자 및 다른 모든 소프트웨어와 하드웨어를 연결하는 소프트웨어 계층

- 협의의 운영체제(커널) - 운영체제의 핵심 부분으로 메모리에 상주하는 부분

- 광의의 운영체제 - 커널 뿐 아니라 각종 주변 시스템 유틸리티를 포함한 개념

![운영체제란](https://user-images.githubusercontent.com/58287684/100165123-c82d9980-2efc-11eb-8c23-2fa1559a65dd.png)



#### 2. 운영체제의 목적

컴퓨터 시스템의 **자원을 효율적**으로 관리

사용자가 컴퓨터 시스템을 **편리하게 사용**할 수 있는 환경을 제공



#### 3. 운영체제의 분류

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



##### [몇 가지 용어 정리]

- `Multitasking`  : 한 컴퓨터에서 여러 작업을 동시의 수행, cpu가 빠르게 돌면서 각각의 task를 번갈아가며 일을 수행 -> 행위 강조
- `Multiprogramming` : 메모리에 여러 프로그램이 동시에 올라간것 -> 메모리 측면을 강조
- `Time sharing` : CPU의 시간을 분할하여 수행 -> 나누어 쓴다는 의미를 강조
- `Multiprocess` : 여러 프로그램이 동시에 수행
- `Multiprocessor` : 하나의 컴퓨터에 여러개의 CPU(processor)가 붙어있음을 의미



#### 4. 운영체제의 구조

- CPU 관리
- 메모리 관리
- 파일 관리
- 입출력 관리 - 인터럽트로 CPU에게 요청함
- 프로세스 관리

![운영체제 기능](https://user-images.githubusercontent.com/58287684/100165080-acc28e80-2efc-11eb-839f-5b41425d0330.png)





## 02. System Structure & Program Execution

#### 1. 컴퓨터 시스템 구조

![image](https://user-images.githubusercontent.com/58287684/100174633-22842580-2f10-11eb-8643-52a899b35115.png)

- `CPU` : 인스트럭션만 실행하는것이 CPU의 숙명. 메모리 몇번지에 있는 일을 하라 라는 것이 적혀있음
  - CPU는 매순간 Memory 어딘가에 올라와 있는 기계어를 처리한다. Instruction(크키 약  4byte)를 읽어서 실행. (기계어를 하나 읽어오고 실행하는 일을 반복적으로 함 Fetch & Execution)
  - Register 중에 메모리 주소를 가르키는 Register가 존재하는데 이를 Program Counter 라고 한다.
  - CPU는 Program Counter 가 가르키는 주소에서 Instruction을 꺼내와서 실행하는 일을 반복적으로 수행
  - Program Counter는 CPU가 하나 꺼내갔을 때, 다음 주소를 가르킨다.
  - Instruction을 읽어서 실행한 후 다음 Instruction을 실행하기전에 Intrrupt가 들어왔는지 체크한다.
  - 만약 Interrupt가 존재한다면 Program Counter가 가르키는 주소에서 Instruction을 가져오는 것이 아니라 지금 하던 작업을 멈추고 CPU를 누가 쓰고있었는지 제어권이 운영체제에게 넘어가게 된다.
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



#### 2. 인터럽트 Interrupt

주변장치와 입출력 장치는 CPU나 메모리와 달리 `인터럽트`라는 매커니즘을 통해 관리한다. 긔 이유는 입출력 연산이 CPU 명령 수행속도보다 현저히 느리기 때문이다. OS악덕사장, CPU고급인력, 입출력직원 (입출력직원이 CPU에게 작업완료를 알려주는 것이 인터럽트!)

- 인터럽트 당한 시점의 레지스터와 program counter를 save한 후 CPU의 제어를 인터럽트 처리 루틴에 넘김
- Interrupt (넓은 의미)
  - Interrupt (**하드웨어 인터럽트**) : 하드웨어가 발생시킨 인터럽트로 CPU가 아닌 다른 하드웨어 장치가 CPU에 어떤 사실을 알려주거나 CPU 서비스를 요청해야 할 경우 발생한다.
    - I/O Controller, Timmer
  - Trap (**소프트웨어 인터럽트**)
    - Exception : 프로그램이 오류를 범한 경우
    - System call : 프로그램이 커널 함수를 호출하는 경우
- 인터럽트 관련 용어
  - 인터럽트 벡터 : 해당 인터럽트의 처리 루틴 주소를 가지고 있음
  - 인터럽트 처리 루틴(=Interrupt Service Routine, 인터럽트 핸들러) : 해당 인터럽트를 처리하는 커널 함수



#### 3. 입출력의 수행

- 모든 입출력 명령은 특권 명령
- 사용자 프로그램은 어떻게 I/O를 하는가?
  - 시스템콜(system call) : 사용자 프로그램은 운영체제에게 I/O 요청
    - 사용자 프로그램이 운영체제의 서비스를 받기 위해 커널 함수를 호출하는 것
  - trap을 사용하여 인터럽트 벡터의 특정 위치로 이동
  - 제어권이 인터럽트 벡터가 가리키는 인터럽트 서비스 루틴으로 이동
  - 올바른 I/O 요청인지 확인 후 I/O 수행
  - I/O 완료시 제어권을 시스템콜 다음 명령으로 옮김



#### 4. 동기식 입출력과 비동기식 입출력

![image](https://user-images.githubusercontent.com/58287684/100188418-7c471880-2f2d-11eb-8570-ca8d2543daaf.png)

- 동기식 입출력 (synchronous I/O : 동시에 일어나는)
  - I/O 요청 후 입출력 작업이 완료된 후에야 제어가 사용자 프로그램에 넘어감 (기다리는 동안 다른일 못함)
  - 구현방법 1 (cpu도 I/O장치도 낭비가 된다.)
    - I/O가 끝날 때까지 CPU를 낭비시킴
    - 매 시점 하나의 I/O만 일어날 수 있음
  - 구현방법 2 (cpu가 놀지 않고 일할 수 있고 아이오 장치도 여러개가 일할 수 있어서 더 효율적)
    - I/O가 완료될 때까지 해당 프로그램에게서 CPU를 빼앗음
    - I/O 처리를 기다리는 줄에 그 프로그램을 줄 세움
    - 다른 프로그램에게 CPU를 줌
- 비동기식 입출력 (asynchronous I/O : 동시에 일어나지 않는)
  - I/O가 시작된 후 입출력 작업이 끝나기를 기다리지 않고 제어가 사용자 프로그램에 즉시 넘어감
- 두 경우 모두 I/O 의 완료는 인터럽트로 알려줌



I/O는 커널을 통해서만 할 수 있다. 사용자 프로그램이 I/O 요청을 운영체제 커널에게 하게 되면 알맞은 드라이버를 통해서 하드웨어로 오고 

사용자가 운영체제 거널에 요청만 하고 작업권을 얻어서 다른작업들을 한다 아이오가 끝난걸 알려주긴한다.

두개의 아이오가 실제로 어떤의미를 가지느냐



#### 5. DMA (Direct Memeory Access)

메모리에 접근할 수 있는 장치는 CPU 밖에 없는데 IO장치들이 CPU와 통신을 할 필요가 있을 때 인터럽트를 걸어주면 CPU가 버퍼에 있는 내용을 메모리에 복사해서 가져오게 된다. IO장치들은 워낙 작고 다양해서 직접 인터럽트를 걸어주게 되면 자주 인터럽트가 발생하게 되고 상당한 오버헤드가 뒤따르게 되며 효율적이지 못하게 된다.

그래서 메모리에 직접 접근할 수 있는 DMA라는 장치를 만들어 놓고 작은 일(block, page단위)들이 요청이 들어오면 버퍼에 있는 내용을 메모리에 복사해놓고 쌓아두다가 일정 크기가 되면 CPU에게 한 번에 인터럽트로 알려줌으로써 CPU가 인터럽트를 당하는 횟수를 줄이고 더 효율적으로 일을 할 수 있게 한다.

CPU의 중재 없이 device controller가 device의 buffer storage의 내용을 메모리에 바이트 단위가 아닌 block 단위로 직접 인터럽트를 발생시킨다. 



#### 6. IO를 할 수 있는 서로 다른 두가지 방법

- Special Instruction (일반적인 I/O 방식)
  - CPU에서 실행할 수 있는 인스트럭션에는 메모리만 접근하는 인스트럭션이 있고, I/O 장치만 접근하는 인스트럭션이 있다.
- Memory Mapped I/O
  - 메모리 주소뿐 아니라 I/O 장치들에게도 메모리주소의 붙여서 메모리 접근하는 인스트럭션을 통해서 IO를 할 수 있게 하는 것이다. 메모리주소의 연장주소를 붙인 후에 IO를 하는 것



#### 7. 저장장치 계층 구조

![image](https://user-images.githubusercontent.com/58287684/100192578-9553c780-2f35-11eb-951b-5a1495089cee.png)

- Primary (Executable)은 CPU가 직접 접근 가능 (CPU 직접 접근 = Byte 단위로 접근)
- Secondary은 CPU가 직접 접근하지 못함 (Sector 단위로 접근 가능)



#### 8. 프로그램 실행 (메모리 Load)

![image](https://user-images.githubusercontent.com/58287684/100193946-29269300-2f38-11eb-98f1-4ed3df9c99c1.png)

프로그램들은 실행파일로 하드디스크에 저장되어있다. 이 실행파일을 실행시키면 메모리에 올라가서 프로세스가 된다.

![image](https://user-images.githubusercontent.com/58287684/100194060-55421400-2f38-11eb-8dca-c4cc6bf6d9e4.png)

정확하게는 이런 프로세스가 물리적 메모리에 바로 올라가지 않고 중간에 `가상메모리`를 거치게 된다. 각 프로그램마다 독자적으로 가지고 있는 주소공간을 가상메모리라고한다. A라는 실행파일을 실행하게 되면 A프로그램의 Address Space 메모리 주소공간(0번지부터 시작)이 형성이 되고 B를 실행시키면 B프로그램의 Address Space 메모리 주소공간(0번지부터 시작)이 형성이 된다. 각 프로그램마다 만들어지는 주소공간은 `코드` `데이터` `스택`으로 구성이 된다. 

- `Code` : 프로그램 기계어 코드
- `Data` : 변수나 전역변수, 자료구조
- `Stack` : 코드가 함수구조로 되어있는데 이 함수를 쌓아두었다가 호출, 리턴

모든 프로그램이 독자적인 주소공간(가상메모리)을 가지고 있는데 이것을 물리적 메모리에 올려서 실행을 시킨다. 물리적 메모리에는 커널이 있고, 프로그램을 실행했을때 생성되는 가상 메모리가 있다. 이때 가상 메모리 전체를 올리게 되면 낭비이므로 당장 필요한 부분(함수)만 물리적 메모리에 올린다. 물리적 메모리에 올라가지 않고 프로그램 종료시까지 보관해야하는 부분에 해당하는 나머지는 Swap Area에 올라가 있다. 

- 파일 시스템은 전원이 나가더라도 유지가 되어있는 비휘발성

- Swap Area는 물리적 메모리 용량의 한계로 메모리 연장 공간으로 사용

각 프로그램마다 0번지부터 시작하는 주소공간이 있고, 물리적인 공간도 0번지부터 시작하는데 가상에는 1000번지 인데 물리에서는 3000일수 있음 이렇게 주소를 변환해주는 계층이 있다 이건 운영체제가 하는게 아니고 하드웨어가 해준다. -> 메모리 관리 부분에 나옴



#### 9. 커널 주소 공간의 내용

운영체제 커널도 사실 하나의 프로그램이기 때문에 마찬가지로 `code` `data` `stack`으로 이루어진 주소공간으로 되어있다.

 ![image](https://user-images.githubusercontent.com/58287684/100196084-b7e8df00-2f3b-11eb-8f97-3dcaf01db1cf.png)



#### 10. 사용자 프로그램이 사용하는 함수

- 사용자 정의함수 : 자신의 프로그램에서 정의한 함수
- 라이브러리 함수
  - 자심의 프로그램에서 정의하지 않고 갖다 쓴 함수
  - 자신의 프로그램의 실행 파일에 포함되어있다.

=> 프로세스의 Address Space의 code에 있음(점프가능)

- 커널함수
  - 운영체제 프로그램의 함수
  - 커널 함수의 호출 = 시스템 콜

=> 커널 Address Space의 code에 있음 (사용자는 접근 불가)

CPU제어권을 변경한 후(시스템콜 : 유저모드 -> 커널모드)에 커널 함수를 실행해야한다.







