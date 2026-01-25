# 1. Concurrency
## 1.1. Concurrency vs Parallelism
- Concurrency
    - 여러 작업을  논리적으로 동시에 실행하는 것처럼 보이게 설계·관리
    - 스케줄링, context switching, 비동기 처리 등을 통해 동작
- Parallelism
    - 여러 코어(또는 머신)를 물리적으로 활용해, 동시에 작업을 수행함으로써 성능(처리량, 응답속도 등)을 향상 시키는 것
    - 한 작업을 여러 부분으로 나누어 동시에 처리하거나, 여러 작업을 배분해 처리하여 전체 처리 시간을 단축
## 1.2. Race Condition
- 여러 프로세스들이 동시에 데이터에 접근하는 상황에서, 어떤 순서로 데이터에 접근하느냐에 따라 결과 값이 달라질 수 잇는 상황
- 공유 데이터의 동시 접근은 데이터의 불일치 문제를 발생시킬 수 있다. 따라서, Race condition을 막고 일관성을 유지하기 위해서는 협력 프로세스 간의 실행 순서를 정해주는 메커니즘인 Synchronization 필요
### 1.2.1. 예시
1. 커널 모드로 수행 중 인터럽트가 발생하는 경우

<img width="773" height="388" alt="Image" src="https://github.com/user-attachments/assets/a6377b07-33f0-4321-8808-e191b9cdde6f" />

- 의도된 동작은 count++, count-- 모두 반영되어 count가 초기값을 유지하는 것이지만, 만약 Load를 한 후에 인터럽트가 발생하는 경우 인터럽트의 결과는 반영되지 않고 coun++만 반영된다.

# 2. Synchronization
- 프로세스 또는 스레드들이 수행되는 시점을 조절하여 서로가 알고 있는 정보가 일치하는 것
## 2.1. Critical Section
- 코드 상에서 Race condition이 발생할 수 있는 특정 부분을 말한다. 즉, 공유 데이터를 접근하는 코드 부분
- Mutual Exclusion, Progress, Bounded Waiting
## 2.2. lock
### 2.2.1. spinlock
- 스레드가 공유자원을 얻을 수 있을 때까지 무한 루프를 돌면서 확인하는 매커니즘
- 대기 중인 스레드가 공유 자원의 상태를 무할 루프를 돌며 확인하는 방식
- busy waiting -> CPU 낭비가 계속됨
- 보통 context switching 시간이 더 짧을 때나 멀티 코어 상태일 때 사용
- 예를 들어, 한 사람이 화장실을 사용하고 있고 다른 사람이 화장실을 이용하려고 할 때 다른 사람은 계속 화장실 앞에서 노크를 하면서 나올때까지 기다리는 상황이다.

```
import java.util.concurrent.atomic.AtomicBoolean;

public class SpinLock {
    private AtomicBoolean isLocked = new AtomicBoolean(false);

    public void lock() {
        // Lock을 얻을 때까지 CPU를 쓰면서 무한 루프 (Busy Waiting)
        while (!isLocked.compareAndSet(false, true)) {
            // 아무것도 안 하고 계속 체크만 함
        }
    }

    public void unlock() {
        isLocked.set(false);
    }
}
```
### 2.2.2. Mutex
- 임계 구역 문제를 해결하기 위한 가장 간단한 방법
- 상호 배제(Mutual Exclusion)을 따르기 때문에 하나의 Lock만 존재한다.
- 공유 자원이 하나일 때 사용하는 동기화 방법
- Lock을 걸고(acquire), 푸는(release) 동작은 atomic하게 수행한다. (Lock을 건 프로세스만 Lock을 풀 수 있다)
- 예를 들어, 한 사람이 화장실을 사용하고 있고 다른 사람이 화장실을 이용하려는 상황이 있다고 가정해보자
    - 이때, 처음 사용하는 사람이 들어가면서 문을 잠근다(Lock)
    - 다른 사람이 화장실을 이용하려고 하면 처음에 문이 잠겨 있는지 확인하고 문을 잠겨 있다면 대기하는 장소에서 대기한다.
    - 먼저 사용하고 있는 사람이 나오면서 잠긴 문을 열어놓고 나간다(release)
    - 문이 열리면 기다리고 있는 사람이 들어가서 문을 잠그고 볼 일을 본다.
- 대기 큐를 생성하여 임계 영역에 스레드가 있을 경우 다른 스레드가 공유 자원을 사용하려고 한다면, 스레드를 Blocking하고 대기 큐에 Sleep한다.
```
import java.util.concurrent.locks.ReentrantLock;

public class MutexExample {
    private final ReentrantLock lock = new ReentrantLock();
    private int count = 0;

    public void increment() {
        lock.lock(); // 열쇠 획득
        try {
            count++; // 임계 구역
        } finally {
            lock.unlock(); // 반드시 해제 (예외 발생 대비)
        }
    }
}
```
### 2.2.3. Semaphore
- 뮤텍스에서 더 고차원적인 동기화 방법이다.
- 멀티 프로세스 환경에서 여러 개의 공유 자원에 대한 접근을 제한하는 방법이다.
- 예를 들어, 최대 3개의 화장실을 사람들이 공동으로 나눠서 쓰는 방법을 생각해보자
    - 이때, 세마포어는 S(정수형)는 남은 화장실 수 = 공유 자원에 접근할 수 있는 프로세스/스레드의 수를 의미한다.
    - 화장실에 들어가면서 사용중인 화장실 수를 나타내는 P 연산
    - 화장실을 모두 사용한 사람이 나오면서 빈 화장실 수를 올리는 V 연산
    - 즉, S가 0이면 모든 사람이 화장실을 사용중이고 남은 화장실 수가 없다는 뜻이다.
- 대기하는 방식에는 Busy Waiting / Block & Wake-up 방식이 있다.
```
import java.util.concurrent.Semaphore;

public class SemaphoreExample {
    // 동시에 3개의 스레드만 허용
    private final Semaphore semaphore = new Semaphore(3);

    public void accessResource() {
        try {
            semaphore.acquire(); // 허가증 획득 (S값 감소)
            System.out.println(Thread.currentThread().getName() + " 입장");
            // 자원 사용 로직
        } catch (InterruptedException e) {
            e.printStackTrace();
        } finally {
            System.out.println(Thread.currentThread().getName() + " 퇴장");
            semaphore.release(); // 허가증 반납 (S값 증가)
        }
    }
}
```
### 2.2.4. monitor
```
public class MonitorExample {
    private int count = 0;

    // 메서드 전체가 모니터 영역이 됨
    public synchronized void increment() {
        count++;
    }

    // 또는 특정 블록만 지정 가능
    public void safeIncrement() {
        synchronized(this) {
            count++;
        }
    }
}
```
# 3. Deadlock
- 두 개 이상의 프로세스가 서로 가진 자원을 기다리며 영원히 멈춰버리는 상태를 의미
## 3.1. 발생 조건
1. 상호배제(Mutual Exclusion)
- 한 번에 하나의 프로세스만 자원을 사용할 수 있음
2. 점유 및 대기(Hold and Wait)
- 프로세스가 이미 할당된 자원을 점유한 채 추가 자원을 기다림
3. 비선점(No Preemption)
- 프로세스가 다른 프로세스의 자원을 강제로 가져올 수 없음
4. 원형 대기(Circular Wait)
- 프로세스 간 자원을 요청하는 순환 구조가 존재
## 3.2. Prevention
1. Mutual Exclusion 
- Critical Section Problem을 해결하기 위해서는 이 조건은 반드시 만족해야 하므로 공유자원이 존재한다면 이 조건은 만족시킬 수밖에 없다. 
2. Hold and Wait
- 프로세스가 자원을 요청할 때 다른 어떤 자원도 가지고 있지 않도록 해야 한다.
- 따라서 프로세스를 시작할 때 모든 필요한 자원을 할당받게 하거나, 자원이 필요한 경우 보유하고 있던 자원을 모두 반납하고 다시 요청하는 방식을 이용할 수 있다.  
3. No preemption
- 프로세스가 어떤 자원을 기다려야 하는 경우 보유하고 있던 자원이 선점된다. 그리고 모든 필요한 자원을 얻을 수 있을 때 그 프로세스는 다시 시작된다. 
4. Circular wait
- 자원의 타입에 따라 프로세스마다 할당 순서를 정하여 정해진 순서대로만 자원을 할당한다.

***

# 참고자료
## Concurrency
https://rebro.kr/176
## Synchronization
https://hello-judy-world.tistory.com/193