# What's Operating System

컴퓨터가 시작될 때 가장 먼저 로드되는 프로그램으로, 다양한 하드웨어 장치를 갖춘 컴퓨터 시스템을 운영하여, 주어진 여러 프로그램이 **Efficiently**하게 실행되도록 하는 프로그램 모음이다. <br>
(응용 프로그램의 구축 및 실행을 지원하며, 응용 프로그램을 위한 기반 환경(Platform) 역할을 수행)

## 1. Motivation

- **Demands :**
  - 프로그램 이식, 기존 프로그램의 결합, 다양한 하드웨어 관리, 대화형 기능(네트워킹) 제공, 정보의 영구 저장 등.

- **Problems :**
  - 하드웨어 의존성으로 인한 이식성(Portability) 문제.
  - 프로그램 간의 상호운용성 및 스케줄링(Scheduling) 문제.
  - 효율성과 확장성을 위한 자원 관리(Resource Management) 문제.
  - 시스템의 안전 및 보안(Safety & Security) 문제.

## 2. Approach

- Virtualization: 컴퓨터 시스템을 가상화하여 애플리케이션과 프로그래머에게 일관되고 단순한 뷰를 제공 

- Common Interface: 응용 프로그램이 하드웨어 및 다른 프로그램과 통신할 수 있는 공통 인터페이스를 제공

- Protection: 하드웨어에 대한 직접적인 접근을 방지하여 시스템을 보호
  - Dual-mode: `User-mode / Kernel-mode`
  - Mode Transition: 응용 프로그램이 하드웨어 자원이 필요할 때 `System Call`을 호출하여 Kernel-mode로 전환

## 3. Solution - Abstraction
OS는 복잡한 하드웨어를 추상 객체로 변환하여 관리한다.

- **Process**
  실행 중인 프로그램의 인스턴스와 그 프로그램이 사용하는 모든 자원을 나타내는 추상 객체

- **Virtual Memory**
  물리적 메모리 위치를 논리적으로 추상화한 것

- **File System**
  Streams을 위한 추상 객체로, 다음과 같은 대상과의 연결을 담당
  - 저장 장치 (영구 메모리)
  - 다른 프로그램
  - 네트워크를 통한 다른 시스템

## 3. System Programs
커널 위에서 실행되며 사용자 및 응용 프로그램이 커널과 쉽게 상호작용할 수 있도록 돕는 프로그램이다.

ex) Compiler, Linker, Loader, Shell, Service Daemons, 등.

---

# Process

**정의:** 프로그램의 실행 중인 인스턴스로 실행 중인 인스턴스에게 주어진 모든 정보와 자원을 포함하는 커널 객체를 뜻한다. <br>
**구성 요소: 크게 Memory Image와 PCB로 나뉜다.**
- Memory Image
  - Code, Data, Heap, Stack Section...etc
- PCB
  - PID, Process State, PC, CPU Registers...etc

## life cycle of process

UNIX에서는 `fork()` system call로 프로세스를 생성할 수 있고, 이렇게 생성된 프로세스의 life cycle은 다음과 같다.

<img width="342" height="370" alt="image" src="https://github.com/user-attachments/assets/f843d8f1-03cb-44cb-a46c-7f5eb79be1e9" />
<img width="335" height="211" alt="image" src="https://github.com/user-attachments/assets/7d537247-d980-4f18-8684-72581f03f1a5" />

각 프로세스는 위와 같은 Process State를 가지게 된다. <br>

또는 아래와 같은 표현으로 process의 life cycle을 표현하기도 한다.

<img width="487" height="214" alt="image" src="https://github.com/user-attachments/assets/fd73a664-1039-48cc-a719-bc029f233945" />

프로세스의 running이 종료되면, wait하거나, terminate 되는데 이때 `exit` system call을 통해 스스로 종료한다. <br>
**하지만 job이 끝나도 종료되지 않은 프로세스를 zombie process**라고 하며, <br>
A parent process can cut off a child process with abort system call 이기 때문에 when the parent quits되어도 **자식은 종료되지 않은 orphan process** 가 존재한다.

---

# Thread

**정의:** 프로세스가 시스템 자원 전체를 아우르는 단위라면, 스레드는 그 안에서 오직 CPU의 실행 흐름만을 추상화한 것이다. <br>
즉, 프로세스 내부의 작업 단위이며 하나의 프로세스는 하나 이상의 스레드를 가지고 실질적인 연산과 로직 수행은 스레드 단위로 이루어진다.

## Process vs Thread

- Process: CPU, 메모리(주소 공간), 파일 시스템 등 모든 시스템 자원을 포함하는 추상화 모델

- Thread: 프로세스가 확보한 자원 중 메모리 공간(Address Space)과 시스템 자원들을 공유하며, 오직 CPU 상태(Program Counter, Registers, Stack)만을 독립적으로 가진다.

- 구조적 차이:
  - 공유 영역: Code(명령어), Data(전역 변수), Heap(동적 할당) 영역은 같은 프로세스 내의 모든 스레드가 공유
  - 독립 영역: 각 스레드는 독립적인 실행 경로를 유지하기 위해 자신만의 Stack과 레지스터 상태를 가진다.

## Multithreading Mechanism

<img width="574" height="286" alt="image" src="https://github.com/user-attachments/assets/d6739e48-4dc5-4af1-8658-ed19554b295d" />

- 스레드 간의 Context Switch은 프로세스 간의 교환보다 오버헤드가 적다. <br>
  (메모리 주소 공간을 그대로 둔 채 CPU 상태만 바꾸면 되기 때문)

- 스레드 역시 실행 중에 하드웨어 자원이 필요하면 System Call을 호출하며, 이 과정에서 User-mode에서 Kernel-mode로의 전환이 발생

---

# Dual Mode Operation: User Mode & Kernel Mode
사용자 프로그램이 하드웨어(디스크, 네트워크 등)에 직접 접근하거나 메모리의 임의 영역을 수정하여 시스템 전체에 문제를 일으키는 것을 방지하기 위해 Dual Mode를 사용한다.

### User Mode

응용 프로그램이 실행되는 일반적인 모드로, 하드웨어 자원에 직접 접근하는 Privileged Instructions의 실행이 금지된다. <br>
(실행하려 하면 하드웨어 수준에서 Exception을 발생)

### Kernel Mode

Privileged Instructions가 실행 가능하여 모든 하드웨어 장치 제어, 메모리 관리, 입출력(I/O) 수행 등 시스템의 모든 자원에 접근 가능한 모드.

### System Call

유저 모드 프로그램이 커널의 서비스를 받기 위해 사용하는 유일한 통로로 Trap을 통해 동작한다.

1. 프로그램이 특정 Trap 명령을 실행
2. 하드웨어는 현재 상태를 커널 스택에 저장하고 Kernel-mode로 전환
3. 미리 정의된 Trap Handler를 통해 요청된 작업을 수행
4. 작업 완료 후 return-from-trap을 통해 유저 모드로 복귀

<img width="397" height="433" alt="image" src="https://github.com/user-attachments/assets/3ecf9d38-5d37-477a-ba05-550d0c4f7090" />

이러한 System Call을 통해 **Context Switch**가 이루어 진다.

# Context Switch

**정의:** 실행중인 process 혹은 thread를 변경하는 작업을 통칭한다.

하나의 프로세스의 작업이 종료되면 다음 프로세스를 실행해야하는데 이때 context switch가 사용된다. <br>
(Scheduling과 같은 상황에서도 발생 하지만 그건 Scheduling에서 다룰 예정)

현재 실행 중인 프로세스의 레지스터 상태를 PCB에 저장하고, 다음 실행할 프로세스의 상태를 복구하는 과정이 커널 모드에서 안전하게 수행한다.

---

# Scheduling

Multi-programming을 위해 한정된 CPU 자원을 여러 프로세스에 효율적으로 할당하는 스케줄링이 꼭 필요하다.

**Scheduling Policy**
- Dispatch Order: Ready Queue에 있는 프로세스 중 어떤 순서로 CPU를 할당할 것인가?
- Time Slice (Quantum): 한 번 할당받은 프로세스에 얼마만큼의 실행 시간을 부여할 것인가?

스케줄러은 위 두 질문에 대해 답해야한다.

**Workload**
시스템에서 실행 중인 프로세스들의 Characteristics을 의미한다. <br>
스케줄링 알고리즘의 효율성은 이 워크로드를 어떻게 정의하느냐에 따라 달라짐

## Scheduling Metrics

어떤 스케줄링 알고리즘을 평가하는 방법은 두 가지 지표로 이루어진다.

지표|	정의|	성격|	수식
|:---:|:---:|:---:|:---:
Turnaround Time|	작업이 완료된 시점과 도착한 시점의 차이|	Performance 위주|	$T_turnaround ​= T_completion ​− T_arrival​$
Response Time|	작업이 도착한 후 처음으로 스케줄링(실행)될 때까지의 차이|	Fairness가 기준 / 대화형 시스템(interaction이 빈번한 시스템에서)|	$T_response​ = T_first_run ​− T_arrival​$

## First In First Out (FIFO) Scheduling Policy

## Shortest Job First (SJF) Scheduling Policy

## Shortest Time-to-completion First (STCF)

## Round Robin (RR) Scheduling Policy

## MLFQ

## Lottery Scheduler

## Stride Scheduling

## The Linux Completely Fair Scheduler (CFS)
