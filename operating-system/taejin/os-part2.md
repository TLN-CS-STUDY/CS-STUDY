# 1. Synchronization

멀티스레딩 환경에서 스레드들은 프로세스의 자원을 공유하며 실행된다. <br>
멀티스레드 프로그램은 동일한 입력에 대해서도 스케줄링 방식에 따라 결과가 달라지는 Non-deterministic 특성이 존재하는데
이때 실행 순서를 제어하지 않으면 프로그램이 우리가 의도한 대로 동작하지 않게 되는 문제가 발생한다.

```c
#include <stdio.h>
#include <pthread.h>

// 모든 스레드가 공유하는 자원
static volatile int counter = 0; [cite: 125]

// 각 스레드가 실행할 함수
void *mythread(void *arg) {
    printf("%s: 시작\n", (char *) arg); [cite: 147, 148]
    for (int i = 0; i < 1e7; i++) { [cite: 157]
        counter = counter + 1; [cite: 160]
    }
    printf("%s: 완료\n", (char *) arg); [cite: 164]
    return NULL;
}

int main() {
    pthread_t p1, p2;
    printf("메인: 시작 (카운터 = %d)\n", counter); [cite: 187, 188]

    // 두 개의 스레드 생성
    pthread_create(&p1, NULL, mythread, "A"); [cite: 190, 191, 192]
    pthread_create(&p2, NULL, mythread, "B"); [cite: 194, 195, 196]

    // 스레드가 종료될 때까지 대기
    pthread_join(p1, NULL); [cite: 202]
    pthread_join(p2, NULL); [cite: 203]

    printf("메인: 종료 (최종 카운터 = %d)\n", counter); [cite: 205, 207]
    return 0;
}
```

위 코드를 실행해보면 매번 counter 값이 달라지는 것을 알 수 있다.

# 2. Race Condition

공유 자원에 여러 스레드가 동시에 접근할 때 발생하는 문제를 race condition이라고 한다.

1.에서 counter 코드를 살펴보면 스레드 A가 값을 증가시킨 후 메모리에 저장하기 직전, 타이머 인터럽트에 의해 스레드 B로 Context Switch가 일어날 수 있기 때문에 스레드 B가 옛날 값을 읽어와서 증가시키면, 결과적으로 스레드 A의 작업이 덮어씌워져 유실되는 것이다. <br>

하나의 예시를 또 봐보자면

<img width="632" height="241" alt="image" src="https://github.com/user-attachments/assets/1198b028-8f54-4987-a6fc-057006b3110e" />

인출 과정에서 balance라는 공유 자원에 대해서도 순서가 잘 지켜지지 않으면 문제가 발생한다.

즉, Critical Section이 Atomically으로 실행되지 않는다는 것이다.

그리고 이를 해결하기 위해 Lock/Mutex, Semaphore, Condition Variable가 존재한다.

# 3. Race Condition Solutions

프로그래머는 non-deterministic한 스케줄링 interrupts에도 atomically하게 명령어를 순서대로 실행시켜야하고, <br>
이를 위한 메커니즘들은 Lock/Mutex, Semaphore, Condition Variable 등이 있다.

## 3.1 Lock

Lock은 특수한 변수로 mutex(mutual exclusion)라고 부르며, 다음과 같은 상태와 명령을 가진다.

- status
  - available (or unlocked, or free)
  - acquired (or locked, or held): owner
- operations
  - lock (or acquisition)
  - unlock(or release)

### 3.1.1. Lock Implementations

Lock의 구현은 단순히 flag 변수로 하면 안된다. <br>
왜냐하면 flag를 확인하는 순간에도 race condition이 발생할 수 있기 때문이다.

그렇다면 critical section에 thread가 들어가면 interrupt를 disable하는 방법은 어떤가? <br>
그러면 아래와 같은 추가적인 문제가 발생한다.

- dangerous
- reduces concurrency
- does not work on multiprocessor architectures
- inefficient

그래서 과거에는 software lock algorithms을 사용했었다.

이 알고리즘들은 두 개의 스레드가 동시에 임계 구역에 진입하지 않도록 보장했지만 또한 문제가 아래와 같이 존재한다.

- 확장성 부족: 스레드 수가 늘어날수록 알고리즘이 기하급수적으로 복잡해진다.
- 멀티프로세서 비호환: 현대의 멀티프로세서 아키텍처에서는 제대로 작동하지 않을 수 있다.
- 성능 저하: CPU가 아무것도 하지 않으면서 무한 루프를 도는 스핀 Spin-wait 방식을 사용하므로 자원 낭비가 심하다.

그래서 현대 OS에서는 Atomic Instructions를 hardware로 부터 받아 사용한다. <br>

- **Test-and-Set:**
메모리 값을 읽는 동시에 새 값을 쓰는 작업을 하나의 원자적 단위로 처리하는 방식으로 lock이 이미 1이면 계속 1을 쓰며 기다리고(Spin-wait 방식), 0이었다면 1로 바꾸면서 이전에 0이었다는 정보를 반환받아 lock 획득에 성공하는 방식

## 3.2. Semaphore

Semaphore는 정수 값을 가진 공유 변수를 이용하여 가용한 자원의 개수를 나타내는 동기화를 진행한다. <br>
Lock이 한 번에 하나의 스레드만 자원에 접근 가능하게 한다면, Semaphore는 (Binary Semaphore 제외, 0과 1로만 이루어져 있어서 lock과 유사함) 여러 스레드가 동시에 자원에 접근할 수 있게 한다.

- **operations**
  - decrease: thread가 resource를 checking out할 때 감소한다.
    (counter가 음수가 되면 block한다.)
  - increase: thread가 resource를 putting back할 때 증가한다.
    (block된 process가 존재하면 wake up 시킨다.)

### 3.2.1 POSIX semaphore

POSIX 표준에서는 위 연산을 다음과 같이 제공한다.

- `sem_wait()` (P 연산): 세마포어 값을 1 감소시킨다. 만약 값이 음수가 되면, 자원이 없다는 뜻이므로 호출한 스레드는 대기(Sleep) 상태로 들어간다.

- `sem_post()` (V 연산): 세마포어 값을 1 증가시킨다. 만약 대기 중인 스레드가 있다면 그중 하나를 깨운다.

<img width="758" height="335" alt="image" src="https://github.com/user-attachments/assets/cec0a362-2fa2-4b25-a544-191d88944d92" />

### 3.2.2. 이진 세마포어와 뮤텍스의 차이

- **소유권 여부:** 뮤텍스는 Lock을 획득한 스레드가 반드시 그 Lock을 해제해야 하는 소유권 개념이 있지만, 세마포어는 소유권이 없으므로 A 스레드가 wait한 세마포어를 B 스레드가 post하여 해제할 수 있다.

- **사용 목적:** 뮤텍스는 오직 한 번에 하나의 스레드만 접근하게 하는 상호 배제가 주 목적이고, 이진 세마포어는 상호 배제뿐만 아니라 두 스레드 간의 실행 순서(Signaling)를 맞추는 용도로도 사용

### 3.2.3. Lock을 얻기 위해 대기하는 프로세스들은 Spin Lock 기법을 사용할 수 있습니다. 이 방법의 장단점은 무엇인가요? 단점을 해결할 방법은 없을까요?

Spin Lock 기법은 `lock()`을 호출했을 때 락을 얻을 때까지 CPU를 계속 사용하며 루프를 도는 기법입니다. <br>
이 기법의 장점은 lock을 얻기 위해 대기할 때 스레드가 잠들지 않으므로, Context Switching overhead가 발생하지 않습니다. <br>
하지만 lock을 아주 짧은 시간만 보유할 것이 확실하다면 효율적이지만 lock을 오래 보유한다면, CPU resource를 100% 점유하며 낭비하기 때문에 기다리는 thread가 cpu를 잡고 있어 시스템이 비효율적으로 동작하는 단점이 존재합니다. <br>
이를 해결하기 위한 방법으로는 Yield과 Sleep/Wake up 방법으로

- Yield: 락을 얻지 못하면 즉시 CPU를 다른 스레드에 양보하여 CPU 낭비를 줄이는 방법
- Sleep/Wakeup: lock을 얻지 못하면 thread를 Sleep 상태로 전환하고 큐에 넣어 관리하고 lock이 해제될 때 커널이 스레드를 wake up하는 방법

## 3.3 Conditional Variable

조건 변수는 실행 상태가 원하는 방향이 아닐 때 스레드가 스스로를 등록하고 대기할 수 있는 Explicit Queue로 조건이 변경되었을 때, 대기 중인 스레드를 깨워 실행을 계속하게 한다.

예를 들어 공유 자원에 접근하기 위한 락은 얻었더라도, 이후 작업에 필요한 특정 조건(예: 버퍼에 빈 공간이 생김)이 만족될 때까지 계속 스핀하며 기다리는 것은 CPU 자원 낭비이고, <br>
이를 conditional variable를 통해 효율적으로 관리할 수 있다.

- operations
  - `wait()`: watting for `signal()`
  - `signal()`

conditional variable은 condition check에서 mutual exclusion을 위해 mutex와 함께 사용된다.

### 3.3.1. Producer-Consumer Problem

conditional variable을 사용하는 예시로 생산자 스레드가 버퍼에 데이터를 넣고, 소비자 스레드가 그 데이터를 꺼내 처리하는 코드이다.

<img width="716" height="401" alt="image" src="https://github.com/user-attachments/assets/74740b8f-a34b-495b-b788-a70ef3a662cb" />

- 생산자(Producer): 데이터를 만들어 버퍼에 넣는다. 버퍼가 가득 찼다면 빈 공간이 생길 때까지 기다린다.
- 소비자(Consumer): 버퍼에서 데이터를 꺼내 처리한다. 버퍼가 비어 있다면 데이터가 들어올 때까지 기다린다.
- 공유 버퍼에 대한 접근은 반드시 Mutual Exclusion가 보장되어야 한다.

#### 3.3.1.1. Producer Logic

1. 임계 구역 보호: `Pthread_mutex_lock(&mutex)`을 통해 버퍼 접근 권한을 얻는다.
2. 상태 확인 (while): `count == MAX`라면 버퍼가 가득 찬 상태로 `Pthread_cond_wait(&empty, &mutex)`를 호출하여 sleep한다.
   이 함수는 대기 상태로 들어가며 atomic하게 락을 해제한다.
4. 데이터 투입: 빈 공간이 생겨 깨어나면 `put(i)`를 통해 데이터를 넣고 `count`를 증가시킨다.
5. 신호 전달: 가득 차게 되면 `Pthread_cond_signal(&fill)`을 호출하여 데이터가 들어오길 기다리던 소비자에게 신호를 보내준다.(깨운다)

#### 3.3.1.2. Consumer Logic

1. 임계 구역 보호: 동일한 뮤텍스로 락을 건다.
2. 상태 확인 (while): `count == 0`이면 꺼낼 데이터가 없으므로,  `Pthread_cond_wait(&fill, &mutex)`를 통해 데이터가 채워질 때까지 sleep한다.
3. 데이터 획득: 신호를 받아 깨어나면 `get()`을 통해 데이터를 꺼내고 count를 감소시킨다.
4. 신호 전달: `Pthread_cond_signal(&empty)`를 호출하여 공간이 부족해 대기하던 생산자를 깨운다.

## 4. Deadlock

이러한 동기화 tool들을 사용하다 보면 두 개 이상의 스레드가 서로 상대방이 보유한 자원을 기다리며 무한히 대기하는 상태인 데드락이 발생할 수 있다.

### 4.1. Coffman Conditions

데드락 발생을 위한 조건은 아래의 4가지가 존재한다. <br>
즉, 아래의 4가지 조건 중 하나라도 예방하면 deadlock을 방지할 수 있는 것이다.

- 상호 배제 (Mutual Exclusion): 자원은 한 번에 하나의 스레드만 사용할 수 있어야 한다.

- 점유 및 대기 (Hold and Wait): 최소한 하나의 자원을 점유한 채로, 다른 스레드에 할당된 자원을 추가로 점유하기 위해 대기하는 스레드가 있어야 한다.

- 비선점 (No Preemption): 다른 스레드에 할당된 자원은 해당 스레드가 스스로 내어놓기 전까지는 강제로 빼앗을 수 없어야 한다.

- 순환 대기 (Circular Wait): 대기 중인 스레드들이 Circle 형태로 서로의 자원을 기다리는 상황이어야 한다.

### 4.2. Deadlock 해결

**1. Prevention:** 
4가지 조건 중 하나를 원천 차단하는 방법이다.

- 순환 대기 방지: 모든 락에 우선순위를 부여하고, 항상 정해진 순서대로만 락을 획득하도록 설계한다.
- 점유 및 대기 방지: 스레드가 실행되기 전 필요한 모든 락을 한꺼번에 획득하게 하거나, 하나라도 얻지 못하면 쥐고 있던 락을 모두 놓게한다.


**2. Avoidance**
실행 시간에 자원 할당 상태를 검사하여 데드락 가능성이 있는 경우 자원 할당을 거부하는 방법이다.

- Banker's Algorithm): 자원을 할당했을 때 시스템이 Safe State를 유지할 수 있는 경우에만 자원을 할당

**3. Detection and Recovery**
데드락 발생을 허용하되, 주기적으로 시스템을 검사하여 데드락이 발견되면 특정 스레드를 강제로 종료하거나 자원을 뺏어 해결하는 방법이다.
- watch dog timer

#### 4.2.1. watch dog timer

시스템이 정상적으로 작동하고 있는지 주기적으로 감시하는 하드웨어 타이머로 소프트웨어 오류(ex. deadlock)를 감지하고 자동으로 시스템을 재시작 시킨다.

**작동 원리: **
1. 타이머 설정: 시스템이 시작될 때 특정 시간(ex. 10s)을 설정하고 카운트다운을 시작
2. 생존 신호 (Heartbeat): 소프트웨어가 정상적으로 작동 중이라면, 타이머가 0이 되기 전에 주기적으로 타이머를 다시 초깃값으로 재설정한다.
   이를 보통 Kicking the Dog 또는 Feeding the Dog 이라고 한다.
3. 시스템 리셋: 만약 데드락이나 오류로 인해 소프트웨어가 타이머를 재설정하지 못해 0에 도달하면, 와치독은 시스템에 하드웨어 리셋 신호를 보낸다.
