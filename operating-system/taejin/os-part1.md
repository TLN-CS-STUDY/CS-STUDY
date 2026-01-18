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

anyway
프로세스의 running이 종료되면, wait하거나, terminate 되는데 이때 `exit` system call을 통해 스스로 종료한다. <br>
**하지만 job이 끝나도 종료되지 않은 프로세스를 zombie process**라고 하며, <br>
A parent process can cut off a child process with abort system call 이기 때문에 when the parent quits되어도 **자식은 종료되지 않은 orphan process** 가 존재한다.

---

# Dual Mode Operation: User Mode & Kernel Mode
