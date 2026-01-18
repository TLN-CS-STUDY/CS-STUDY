# Process
## Job vs Process
### Job/Program
- 실행할 프로그램 + 데이터
- 컴퓨터 시스템에 실행 요청 전의 상태
### Process
- 실행을 위해 시스템(커널)에 등록된 작업
- 시스템 성능 향상을 위해 커널에 의해 관리 됨
## 정의
- 실행중인 프로그램
    - 커널에 등록되고 커널의 관리하에 있는 작업
    - 각종 자원들을 요청하고 할당 받을 수 있는 개체
    - 프로세스 관리 블록(PCB)을 할당 받은 개체
    - 능동적인 객체(active entity)
        - 실행 중에 각종 자원을 요구, 할당, 반납하며 진행

<img width="956" height="422" alt="Image" src="https://github.com/user-attachments/assets/fb466bae-369a-47e1-bd8b-a5c7446fa2d2" />

## Resource
- 커널의 관리 하에 프로세스에게 할당/반납 되는 수동적 개체
- 자원의 분류
    - H/W resources
        - Processor, memory, disk, monitor, keyboard, ...
    - S/W resourcess
        - Message, signal, files, installed SWs, ...
## Process Control Block(PCB)
- 커널 공간 내에 존재
- 각 프로세스들에 대한 정보를 관리
- 프로세스 생성 시 생성됨
## Process States
<img width="887" height="293" alt="Image" src="https://github.com/user-attachments/assets/9d89c0e6-8f3e-4dbd-9d73-687b4c5d299f" />

### Created State
- Job을 커널에 등록
- PCB 할당 및 프로세스 생성
- 커널
    - 가용 메모리 공간 체크 및 프로세스 상태 전이
        - Ready or Suspended ready
### Ready State
- 프로세서 외에 다른 모든 자원을 할당 받은 상태
    - 프로세서 할당 대기 상태
    - 즉시 실행 가능 상태
- Dispatch(or Schedule)
    - Ready State -> running state
### Running State
- 프로세서와 필요한 자원을 모두 할당 받은 상태
- Preemption
    - Running state -> ready states
    - 프로세서 스케줄링 (time-out, priority changes)
- Block/sleep
    - Running state -> asleep state
    - I/O 등 자원 할당 요청
### Blocked/Asleep State
- 프로세서 외에 다른 자원을 기다리는 상태
    - 자원 할당은 system call에 의해 이루어짐
- Wake-up
    - Asleep state -> ready state
## Suspended State
- 메모리를 할당 받지 못한(뺏긴) 상태
    - Memory image를 swap device에 보관
    - 커널 또는 사용자에 의해 발생
- Swap-out(suspended), Swap-in(resume)
## Terminated/Zombie State
- 프로세스 수행이 끝난 상태
- 모든 자원 반납 후,
- 커널 내에 일부 PCB 정보만 남아 있는 상태
    - 이후 프로세스 관리를 위해 정보 수집
## Process State Transition Diagram
<img width="1401" height="747" alt="Image" src="https://github.com/user-attachments/assets/afdb8fb9-dbb9-4eac-b903-285f782cce6e" />

# Interrupt
- 예상치 못한, 외부에서 발생한 이벤트
    - Unexpected, external events
## 처리 과정
<img width="789" height="340" alt="Image" src="https://github.com/user-attachments/assets/0ea7881b-e463-4b56-9baa-3b2ae19a2ebf" />

<img width="722" height="479" alt="Image" src="https://github.com/user-attachments/assets/09f987b4-b857-41b4-be47-9d6ccc9043bc" />

## Context Switching
- Context
    - 프로세스와 관련된 정보들의 집합
- Context saving
    - 현재 프로세스의 Register context를 저장하는 작업
- Context restoring
    - Register context를 프로세스로 복구하는 작업
- Context switching
    - 실행 중인 프로세스의 context를 저장하고, 앞으로 실행 할 프로세스의 context를 복구 하는 일

***

# Thread
- precess 내부에서 실행되는 작은 작업 단위
## 장점
- 사용자의 응답성(Responsiveness)
    - 일부 스레드의 처리가 지연되어도, 다른 스레드는 작업을 계속 처리 가ㅡㅇ
- 자원 공유(Resource sharing)
    - 자원을 공유해서 효율성 증가(커널의 개입을 피할 수 있음)
- 경제성(Economy)
    - 프로세스의 생성, context switch에 비해 효율적
- 멀티 플세서(multi-processor) 활용
    - 병렬처리를 통해 성능 향상
## 구현
### 사용자 수준 스레드 (User Threads)
- 사용자 영역의 스레드 라이브러리로 구현
    - 스레드의 생성, 스케줄링 등
    - POSIX threads, Win32 threads, Java thread API 등
- 커널은 스레드의 존재를 모름
    - 커널의 관리(개입)를 받지 않음
    - 커널은 프로세스 단위로 자원 할당
<img width="708" height="422" alt="Image" src="https://github.com/user-attachments/assets/89aa70c4-5827-4685-ace2-e7241a4a7d4a" />

### 커널 수준 스레드 (Kernel Threads)
- OS(Kernel)이 직접 관리
- 커널 영역에서 스레드의 생성, 관리 수행
    - Context switching 등 부하(Overhead)가 큼
- 커널이 각 스레드를 개별적으로 관리
    - 프로세스 내 스레드들이 병행 수행 가능S
<img width="706" height="412" alt="Image" src="https://github.com/user-attachments/assets/618356bd-fa27-49a4-b30e-1620be5246a0" />

### Language-level Threads
- Java Threads
    - Java Virtual Machine (JVM)에 의해 생성 관리 됨
### Multi-Threading Model
- 다대일 모델
    - 사용자 수준 스레드
- 일대일 모델
    - 커널 수준 스레드
- 다대다 모델
    - 혼합형 스레드
### 혼합형(n:m) 스레드
- n개 사용자 수준 스레드 - m개의 커널 스레드 (n > m)
    - 사용자는 원하는 수만큼 스레드 사용
    - 커널 스레드는 자신에게 할당된 하나의 사용자 스레드가 block 상태가 되어도, 다른 스레드 수행 가능
- 효율적이면서도 유연함
<img width="633" height="401" alt="Image" src="https://github.com/user-attachments/assets/0b2b2362-8ef6-42ab-a545-ccc1215d2cff" />

***

# Scheduling
- 시스템 내의 프로세스 처리 순서 결정
## Multi-programming
- 여러개의 프로세스가 시스템 내 존재
- 자원을 할당할 프로세스를 선택
- 자원 관리
    - 시간 분할(time sharing) 관리
    - 공간 분할(spance sharing) 관리
## 목적
- 시스템 성능 향상
- 대표적 시스템 성능 지표 (index)
    - 응답 시간(response time)
        - 작업 요청으로부터 응답을 받을떄까지의 시간
    - 작업 처리량(throughput)
        - 단위 시간 동안 완료된 작업의 수
    - 자원 활용도(resource utilizaiton)
        - 주어진 시간동안 자원이 활용된 시간
- 목적에 맞는 지표를 고려하여 스케줄링 기법 선택
## 기준(Criteria)
- 스케줄링 기법이 고려하는 항목들
- process의 특성
- 시스템 특성
- 프로세스의 긴급성(urgency)
- 프로세스 우선순위(priority)
- 프로세스 총 실행 시간(total service time)
## 단계(Level)
- 