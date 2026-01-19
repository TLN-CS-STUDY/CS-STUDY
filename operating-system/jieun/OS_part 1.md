# 1. Operating Systems
## 운영체제(Operating Systems, OS) 란?
- 컴퓨터 시스템의 핵심 소프트웨어로, 컴퓨터 하드웨어와 응용 프로그램 간의 상호작용을 관리하고 제어하는 역할을 한다.
- 사용자와 하드웨어 사이의 인터페이스를 제공해 효율적으로 응용 프로그램이 동작하도록 지원하고, 시스템 자원을 효율적으로 관리하여 응용 프로그램이 원활하게 동작할 수 있도록 한다.
- 일반적으로 커널에 여러가지 기능(라이브러리, 시스템 프로그램 등)이 추가된 상태를 통칭해서 운영체제(OS)라고 한다.

## 운영체제의 구조
운영체제의 구조는 크게 커널(Kernel)과 셸(Shell)로 나눌 수 있다.

### 커널(Kernel)
- 운영체제의 핵심 부분으로 하드웨어와 응용 프로그램 간의 상호 작용을 관리한다.
- 최상위 권한을 가지고 있어 하드웨 자원에 직접 접근하고 응용 프로그램이 원활하게 실행될 수 있도록 한다.
- **주요 기능**: 프로세스 관리, 메모리 관리, 입출력 관리, 파일 시스템 관리 등

### 셸(Shell)
- 사용자와 운영체제 간의 인터페이스 역할을 수행한다.
- 셸은 명령어 해석기(Parser)와 실행기(Executor)로 구성되어 사용자의 명령을 분석하고 실행한다.
- 사용자는 셸을 통해 **운영체제와 상호작용하고 작업을 수행**할 수 있으며, 커널을 호출해 운영체제 기능과 서비스를 조작할 수 있다.

### 시스템 콜(System Call)
- 응용 프로그램에서 운영체제 서비스를 필요로 할 때 사용하는 호출이다.

# 2. Process
## Job vs Process
- 작업(Job) / 프로그램(Program)
	- 실행할 **프로그램 + 데이터**
	- 컴퓨터 시스템에 실행 요청 전의 상태
- 프로세스(Process)
	- 실행을 위해 시스템(커널)에 등록된 작업
	- 시스템 성능 향상을 위해 커널에 의해 관리 됨

<img width="447" height="325" alt="2  프로그램과 프로세스" src="https://github.com/user-attachments/assets/ea0bf49d-6f9d-4371-a368-2833d1e8be40" />

프로그램이 메모리로 적재되면 프로세스가 된다.

## Process 란?
- 실행중인 프로그램을 말한다.
	- 커널에 등록되고 커널의 관리하에 있는 작업
	- 각종 자원들을 요청하고 할당 받을 수 있는 개체
	- 프로세스 관리 블록(PCB)을 할당 받은 개체
	- 능동적인 개체(Active Entity)
		- 실행 중에 각종 자원을 요구, 할당, 반납하며 진행된다.
- Process Control Block (PCB)
	- 커널 공간 (Kernel Space) 내에 존재한다.
	- 각 프로세스들에 대한 정보를 관리한다.

## 종류
|구분|종류|설명|
| :---: | :---: | :---: |
|역할|시스템(커널) 프로세스|모든 시스템 메모리와 프로세서의 명령에 액세스할 수 있는 프로세스이다. 프로세스 실행 순서를 제어하거나 다른 사용자 및 커널(운영체제) 영역을 침범하지 못하게 감시하고, 사용자 프로세스를 생성하는 기능을 한다.|
||사용자 프로세스|사용자 코드를 수행하는 프로세스이다.|
|병행 수행 방법|독립 프로세스|다른 프로세스에 영향을 주지 않거나 다른 프로세스의 영향을 받지 않으면서 수행하는 병행 프로세스이다.|
||협력 프로세스|다른 프로세스에 영향을 주거나 다른 프로세스에서 영향을 받는 병행 프로세스이다.|

## 자원(Resource)의 개념
- 커널의 관리 하에 프로세스에게 할당/반납되는 수동적 개체(Passive Entity)이다.
- 자원의 분류
	- H/W Resources
		- Processor, memory, disk, monitor, keyboard, Etc.
	- S/W Resources
		- Message, signal, files, installed SWs, Etc.
		
## Process Control Block (PCB)
- OS가 프로세스 관리에 필요한 정보를 저장한다.
- 프로세스 생성 시 생성된다.

<img width="671" height="410" alt="3  PCB" src="https://github.com/user-attachments/assets/176ec9f5-6890-4d41-a42d-fa196852fe06" />

CPU는 한 프로세스가 종료될 때까지 수행하는 것이 아니라 여러 프로세스를 중간 중간에 바꿔가면서 수행한다. 그러므로 CPU는 수행중인 프로세스를 나갈 때, 해당 프로세스의 정보를 어딘가에 저장하고 있어야 다음에 이 프로세스를 수행할 대 이전에 수행한 그 다음부터 이어서 작업할 수 있다. 이러한 정보를 저장하는 곳이 PCB이다.
	
### PCB가 관리하는 정보
- PID: Process Identification Number
	- 프로세스 고유 식별 번호
- 스케줄링 정보
	- 프로세스 우선순위 등과 같은 스케줄링 관련 정보들
- 프로세스 상태
	- 자원 할당, 요청 정보 등
- 메모리 관리 정보
	- Page table, Segment Table 등
- 입출력 상태 정보
	- 할당 받은 입출력 장치, 파일 등에 대한 정보 등
- 문맥 저장 영역 (Context save area)
	- 프로세스의 레지스터 상태를 저장하는 공간 등
- 계정 정보
	- 자원 사용 시간 등을 관리

※ 특징 
- PCB 정보는 OS 별로 서로 다르다.
- PCB 참조 및 갱신 속도는 OS의 성능을 결정 짓는 중요한 요소 중 하나이다.

## 프로세스 상태
- 프로세스와 자원 간의 상호작용에 의해 결정된다.
- **프로세스 상태 및 특성**

<img width="650" height="212" alt="4  프로세스 상태 및 특성" src="https://github.com/user-attachments/assets/f46b6f91-c725-446c-ab20-fd44940c9b60" />

**Process State Transition Diagram**

<img width="940" height="221" alt="1  프로세스 상태" src="https://github.com/user-attachments/assets/a81b7747-7e87-4d4c-88f3-54678a43675d" />

### Created State
- 작업(Job)을 커널에 등록한다.
- PCB 할당 및 프로세스를 생성한다.
- 커널
	- 가용 메모리 공간 체크 및 프로세스 상태 전이
		- Ready or Suspended ready

### Ready State
- 프로세서 외에 다른 모든 자원을 할당 받은 상태이다.
	- 프로세서 할당 대기 상태
	- 즉시 실행 가능 상태
- Dispatch (or Schedule)
	- Ready State -> Running State

### Running State
- 프로세서와 필요한 자원을 모두 할당 받은 상태이다.
- Preemption
	- Running State -> Ready States
	- 프로세서 스케줄링(e.g, time-out, priority changes)
- Block/sleep
	- Running State -> Asleep State
	- I/O 등 자원 할당 요청

### Block/Asleep State
- 프로세서 외에 다른 자원을 기다리는 상태이다.
	- 자원 할당은 System call에 의해 이루어진다.
- Wake-up
	- Asleep -> Ready State

### Suspended State
- 메모리를 할당 받지 못한(빼앗긴) 상태이다.
	- Memory image를 Swap Device에 보관한다.
		- Swap Device: 프로그램 정보 저장을 위한 특별한 파일 시스템
- Swap-out(suspended), Swap-in(resume)

### Terminated/Zombie State
- 프로세스 수행이 끝난 상태이다.
- 모든 자원 반납 후, 커널 내에 일부 PCB 정보만 남아있다.
	- 이후 프로세스 관리를 위해 정보를 수집한다.

## 문맥 교환 (Context Switch) 이란?
- 하나의 프로세스가 이미 CPU를 사용 중인 상태에서 다른 프로세스가 CPU를 사용하기 위해 이전 프로세스의 상태를 저장하고 새로운 프로세스의 상태를 적재하는 것이다.
- CPU가 동시에 여러 개의 프로세스를 실행시키는 것처럼 보이지만, 사실은 CPU가 재빠르게 여러 프로세스를 번갈아가며 실행하고 관리하고 있는 것이다. 이때 프로세스를 번갈아가면서 처리하는 것을 **Context Switching(문맥 교환)이라고 한다.

## Context Switching
- **Context**
	- 프로세스와 관련된 정보들의 집합이다.
- **Context saving**
	- 현재 프로세스의 Register Context를 저장하는 작업이다.
- **Context Restoring**
	- Register Context를 프로세스로 복구하는 작업이다.
- **Context Swtiching**
	- 실행 중인 프로세스의 Context를 저장하고, 앞으로 실행할 프로세스의 Context를 복구하는 일이다.
		- 커널의 개입으로 이루어진다.

# 3. Thread
## Thread 란?
- 프로세스 내부에서 실행되는 작은 작업 단위이다.
- 프로세스가 할당받은 자원을 이용하는 실행 흐름을 구성하는 단위로, **하나의 프로세스는 내부에 여러 개의 스레드가 포함**될 수 있다.

## 특징
- 프로세스 내부에 존재하기에 프로세스의 데이터 영역에 접근이 가능하고, 스레드끼리 서로의 데이터에 접근이 가능하다.
- 프로세스처럼 작업을 병렬로 처리해서 속도를 높일 수 있다.
- 스레드의 메모리 영역인 Thread Stack 공간을 가진다.
- 하나의 프로세스는 내부에 여러 개의 스레드를 가질 수 있다.

## 장점
- 사용자 응답성 (Responsiveness)
	- 일부 스레드의 처리가 지연되어도, 다른 스레드는 작업을 계속 처리할 수 있다.
- 자원 공유 (Resource sharing)
	- 자원을 공유해서 효율성이 높아진다. (커널의 개입을 피할 수 있다.)
- 경제성 (Economy)
	- 프로세스의 생성, context switch에 비해 효율적이다.
- 멀티 프로세서 (Multi-Processor) 활용
	- 병렬처리를 통해 성능이 향상된다.

## Thread의 구현
- **사용자 수준 스레드 (User Threads)**
	- 사용자 영역의 스레드 라이브러리로 구현된다.
		- 스레드의 생성, 스케줄링 등
	- 커널은 스레드의 존재를 모른다.	
		- 커널의 관리(개입)을 받지 않는다.
		- 생성 및 관리의 부하가 적고, 유연한 관리가 가능하다.
		- 이식성(portability)이 높다.
	- 커널은 프로세스 단위로 자원을 할당한다.
		- 하나의 스레드가 block 상태가 되면, 모든 스레드가 대기한다.
- **커널 수준 스레드 (Kernel Threads)**
	- OS(Kernel)이 직접 관리한다.
	- 커널 영역세어 스레드의 생성과 관리를 수행한다.
	- 커널이 각 스레드를 개별적으로 관리한다.

# 3. Scheduling
## Multi-Programming
- 여러 개의 프로세스가 시스템 내에 존재한다.
- 자원을 할당할 프로세스를 선택해야 한다. -> 스케줄링(Scheduling)
- 자원 관리
	- 시간 분할(Time Sharing) 관리
		- 하나의 자원을 여러 스레드들이 번갈아가며 사용한다.
		- **프로세스 스케줄링(Process Scheduling)**: 프로세서 사용시간을 프로세스들에게 분배한다.
	- 공간 분할(Space sharing) 관리
		- 하나의 자원을 분할하여 동시에 사용한다.

## Scheduling 이란?
- CPU 스케줄러는 프로세스가 생성된 후 종료될 때까지 모든 상태 변화를 조정하는 일을 한다.
- 스케줄러는 하나의 관리자로 프로세스들의 여러 상황을 고려하여 CPU와 시스템 자원을 어떻게 배정할 지 결정하는 역할을 한다.
- CPU가 하나의 프로세스 작업이 끝난 후 다음 프로세스 작업을 수행해야 하는데, 이때 다음 프로세스가 어느 프로세스인지를 선택하는 알고리즘을 CPU Scheduling 알고리즘이라고 한다.

## Scheduling Criteria
Scheduling Criteria(척도)는 스케줄링의 효율을 분석하는 기준이다.
- 프로세스(Process)의 특성: I/O-bounded or Compute-bounded
- 시스템 특성: Batch System or Interactive System
- 프로세스의 긴급성(Urgency): Hard or Soft-real time, Non-real time systems
- 프로세스 우선순위(Priority)
- 프로세스 총 실행 시간(Total Service Time)
- ...

### CPU burst VS I/O burst
- 프로세스 수행 = CPU 사용 + I/O 대기
- CPU burst: CPU 사용 시간
- I/O burst: I/O 대기 시간
- Burst time은 스케줄링의 중요한 기준 중 하나이다.

## Preemptive VS Non-Preemptive
### Preemptive
Preemptive(선점)은 프로세스가 CPU를 점유하고 있는 동안 I/O나 인터럽트가 발생한 것도 아니고 모든 작업을 끝내지도 않았는데, 다른 프로세스가 해당 **CPU를 강제로 점유** 할 수 있다. <br>
즉, 프로세스가 정상적으로 수행 중인 가운데 다른 프로세스가 CPU를 강제로 점유하여 실행할 수 있는 것이다.

### Non-Preemptive
Non-Preemptive(비선점)은 한 프로세스가 한 번 CPU를 점유했다면, I/O(프로세스 상태가 실행 -> 대기로 변경되는 경우) 또는 프로세스가 종료될 때까지 다른 프로세스가 CPU를 점유하지 못하는 것이다.

## Basic Scheduling Algorithms
### First-Come, First-Served(FCFS)
먼저 온 프로세스가 먼저 CPU를 점유하는 방식이다.

**Gantt Chart**
|Process|Burst Time(msec)|
| :---: | :---: |
|P1|24|
|P2|3|
|P3|3|

<img width="500" height="61" alt="1  FCFS" src="https://github.com/user-attachments/assets/613fd816-e5ca-4af4-82a6-3413f9171650" />

첫 번째 표는 3개의 프로세스와 각 프로세스가 CPU를 사용한 시간(burst time)을 나타낸다. 이를 간트 차트로 표현하면 위와 같다. (도착 시간은 모두 0초라고 가정한다.) <br>
평균 대기 시간은 아래와 같다.

- Average Wating Time = (0+24+27)/3 = 17msec 

만약, 프로세스가 들어온 순서가 `P3, P2, P1`이라면 간트 차트는 아래와 같이 바뀔 것이다. <br>

<img width="500" height="58" alt="2  FCFS_2" src="https://github.com/user-attachments/assets/d170a606-f30f-4b92-8921-dd43b67b2f22" />

- Average Wating Time = (6+3+0) = 3msce

프로세스가 끝난 시간은 30msec로 동일하지만, 평균 대기시간으로 봤을 때 차이가 난다. 즉, 들어온 순서로 수행한다고 해도 반드시 효율적인 것은 아닌 것을 알 수 있다. FCFS는 **Non-Preemptive** 이므로, 하나의 프로세스가 끝나기 전에는 다른 프로세스가 중간에 끼어들 수 없다.

### Shortest-Job-First(SJF)
가장 짧게 수행되는 프로세스가 가장 먼저 수행되는 것을 말한다.

**Gantt Chart**
|Process|Burst Time(msec)|
| :---: | :---: |
|P1|6|
|P2|8|
|P3|7|
|P4|3|

<img width="500" height="65" alt="3  SJF" src="https://github.com/user-attachments/assets/93ee6e47-6e6f-4d99-bad4-eca2d5eb076e" />

위 간트 차트는 SJF를 사용하여 나타낸 것이다. 여기서 평균 대기시간을 계산하면 다음과 같다.

- Average Wating Time = (3+16+9+0)/4 = 7msec

위 표를 FCFS를 사용해서 간트 차트를 나타낸 것이다.

<img width="500" height="70" alt="4  SJF_2" src="https://github.com/user-attachments/assets/85204f13-e3b9-4963-96c6-7d708fb5e6f5" />

- Average Wating Time = (0+6+14+21)/4 = 10.25msec

SJF와 FCFS의 평균 대기시간을 살펴보면 SJF가 더 짧은 것을 볼 수 있다. 이미 수학적으로 증명된 것으로 어떠한 예제를 보더라도 SJF의 AWT가 가장 짧다. <br>
하지만 이 스케줄링 방법은 매우 비현실적이다. 현실적인 컴퓨터 환경에서는 프로세스의 CPU 점유 시간을 알 수 없다. <br>
SJF는 Preemptive와 Non-Preemptive 둘 다 사용 가능하다.

### Priority
우선 순위가 높은 프로세스가 먼저 선택되는 스케줄링 알고리즘이다. 운영체제에서 일반적으로 우선 순위는 정수 값으로 나타내며, 작은 값이 우선 순위가 더 높다.

**Gantt Chart**
|Process|Burst Time(msec)|Priority|
| :---: | :---: | :---: |
|P1|24|3|
|P2|3|1|
|P3|3|4|
|P4|1|5|
|P5|5|2|

<img width="500" height="77" alt="5  Priority" src="https://github.com/user-attachments/assets/4a0f8736-4e4c-4274-be4c-7a025cfaa08b" />

표에서 우선 순위 값이 가장 낮은 순서대로 수행한 모습을 간트 차트로 나타내었다.
 - Average Wating Time = (6+16+18+1)/5 = 8.2msec

우선 순위를 정하는 방법은 크게 내부적인 요소와 외부적인 요소 두 가지로 나뉜다.

- Internal: time limit, memory requirement, I/O to CPU burst
- External: amount of funds being paid, political factors 등

Priority 스케줄링 역시 Preemptive와 Non-Preemptive 두 방식 모두 사용할 수 있다. <br>

Priority 스케줄링의 문제점은 Starvation(기아)가 있다. Starvation은 말 그대로 CPU의 점유를 오랫동안 하지 못하는 현상을 말한다. <br>
우선 순위가 매우 낮은 프로세스가 Ready Queue에서 대기하고 있다고 가정할 대, 이 프로세스는 아무리 오래 기다려도 CPU를 점유하지 못할 가능성이 매우 크다. 새로운 프로세스가 자주 Ready Queue에 들어올 때, 해당 프로세스가 모두 우선 순위가 높은 상태면 이미 기다리고 있던 우선 순위가 낮은 프로세스는 계속 기다리고 있는 상태로 남을 수 있다. <br>

이를 해결하기 위한 방법 중 하나는 **aging**이 있다. Ready Queue에서 기다리는 동안 일정 시간이 지나면 우선 순위를 일정량 높여주는 것이다. 그러면 우선 순위가 매우 낮은 프로세스라 하더라도, 기다리는 시간이 길어질 수록 우선 순위도 계속 높아지므로 수행될 가능성이 커진다.

### Round-Robin(RR)
원 모양으로 모든 프로세스가 돌아가며 스케줄링하는 것을 말한다. 시분할 시스템에서 주로 사용하는 방식이다. <br>
일정 시간을 정하여 하나의 프로세스가 이 시간 동안 수행하고 다시 대기 상태로 돌아간다. 그리고 다음 프로세스가 역시 같은 시간 동안 수행한 후 대기한다. 이러한 작업을 모든 프로세스가 돌아가면서 수행하며, 마지막 프로세스가 끝나면 다시 처음 프로세스로 돌아와 반복한다. <br>

일정 시간을 Time Quantum(Time Slice)이라 부른다. 일반적으로 10 ~ 100 msec 사이의 범위를 갖는다. <br>
Round-Robin은 기본적으로 **Preemptive**이다. 한 프로세스가 종료되기 전에 Time Quantum이 끝나면 다른 프로세스로 CPU를 넘겨주기 때문이다.


**Gantt Chart**
|Process|Burst Time(msec)|
| :---: | :---: |
|P1|24|
|P2|3|
|P3|3|
- Time Quantum = 4msec

<img width="500" height="66" alt="6  RR" src="https://github.com/user-attachments/assets/c6064f28-936b-448f-b851-5495f94e664c" />

RR 방식에서는 Time Quantum이 끝나면 CPU는 현재 프로세스를 대기 상태로 보내고 다음 프로세스를 수행한다.

- Average Wating Time = (6+4+7)/3 = 5.66msec

RR 방식은 Time Quantum 크기에 따라 AWT와 같은 스케줄링 척도가 바뀐다. 그러므로 RR 방식은 *Time Quantum**에 매우 의존적인 것을 알 수 있다. <br>

* * *

**참고 자료** <br>
https://jerryjerryjerry.tistory.com/171 <br>
https://jerryjerryjerry.tistory.com/184 <br>
https://velog.io/@codemcd/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9COS-7.-%EC%93%B0%EB%A0%88%EB%93%9CThread <br>
https://velog.io/@codemcd/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9COS-6.-CPU-%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81 <br>
