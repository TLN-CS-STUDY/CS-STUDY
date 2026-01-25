# 1. Concurrency
## Concurrency VS Parallelism

|Concurrency(동시성)|Parallelism(병렬성)|
| :---: | :---: |
|동시에 실행되는 것처럼 보이는 것|실제로 동시에 실행되는 것|
|논리적인 개념|물리적인 개념|
|싱글코어, 멀티코어에서 가능|멀티코어에서만 가능|

### Parallelism
Parallelism은 여러 코어에서 여러 작업을 동시에 수행하는 것이다. 코어가 하나 밖에 없다면 병렬적으로 프로그램을 실행할 수 없다. 여러 코어에서 여러 작업을 동시에 수행하면서 성능을 올리기 위해서 Multi-Core 체제를 사용한다. <br>

<img width="768" height="405" alt="Image" src="https://github.com/user-attachments/assets/db20d940-cc4d-4e7f-9e9a-fe9d0cb905a9" />

하지만 여러 작업을 동시에 수행하여 **Race Condition** 혹은 **동기화 문제**가 발생할 수 있다. <br>

### Concurrency
Concurrency는 빠르게 전환하며 여러 작업을 수행하여 동시에 여러 작업이 실행되는 것처럼 보이는 것이다. 한 개의 코어에서도 여러 작업을 Concurrent하게 실행할 수 있고 작업 간에는 Context Switch가 일어난다.

<img width="771" height="417" alt="Image" src="https://github.com/user-attachments/assets/79de9ae7-326d-4741-9412-1d15fe878064" />

Task가 동시에 수행되면서 **동기화 문제**가 발생할 수 있다.

## 동기화 문제
동기화 문제는 여러 작업이 동시에 공유된 자원에 접근하려 할 때 발생한다. 멀티코어뿐만 아니라 싱글코어에서 동시에 동작하는 Task 사이에서도 동기화 문제가 발생한다. <br>

# 2. Synchronization
## Synchronization
- 다중 프로그래밍 시스템
	- 여러 개의 프로세스들이 존재하고 프로세스들은 서로 독립적으로 동작한다.
	- 공유 자원 또는 데이터가 있을 때, 문제가 발생할 가능성이 있다.

- 동기화(Synchronization)
	- 프로세스들이 서로 동작을 맞추고 정보를 공유하는 것이다.

## Terminologies
- **Shared data (공유 데이터)**
	- 여러 프로세스들이 공유하는 데이터이다.
- **Critical Section (임계 구역)**
	- 공유 데이터에 접근하는 코드 영역(Code Segment)이다.
- **Mutual Exclusion (상호배제)**
	- 둘 이상의 프로세스가 동시에 Critical Section에 진입하는 것을 막는 것이다.
- **Race Condition**
	- 여러 프로세스들이 동시에 데이터에 접근하는 상황에서, 어떤 순서로 데이터에 접근하느냐에 따라 결과 값이 달라질 수 있는 상황을 말한다.

공유 데이터의 동시 접근(Concurrent Access)은 공유되는 데이터의 작업 처리 순서(연산 순서)에 따라 최종 결과가 달라지기 때문에, 요청된 순서대로 처리하지 않으면 최종 결과의 정확성을 보장하지 못한다. 따라서, Race Condition을 막고 일관성을 유지하기 위해서는 협력 프로세스 간의 실행 순서를 정해주는 메커니즘인 **동기화(Synchronization)**가 필요하다. <br>

## 임계 구역 문제(Critical Section Problem)
n 개의 프로세스가 있는 시스템에서 각 프로세스는 **임계 구역(Critical Section)**이라고 부르는 코드를 포함하고 있고, 그 안에서는 다른 프로세스와 공유하는 변수를 변경하는 등의 작업을 수행한다. <br>

임계 구역 문제(Critical Section Problem)의 목적은 프로세스들이 협력할 때 사용할 수 있는 프로토콜을 설계하는 것이다. <br>

각 프로세스는 자신의 임계 구역으로 진입하기 위해 허가를 요청하는데, 이러한 요청을 구현하는 코드 부분을 **진입 구역(Entry Section)**이라고 하며, 임계 구역 뒤에는 **퇴출 구역(Exit Section)이 있을 수 있다. 코드의 나머지 부분은 **나머지 구역(Remainder Section)**이라고 한다.

## Critical Section Problem 해결 방안
Critical Section Problem를 해결하는 단순한 방법은 `Lock`을 사용하는 것이다. 즉, 한 프로세스가 CS에 들어간다면 Lock을 걸어 다른 프로세스가 들어오지 못하게 하는 것이다. <br>

그리고 프로세스가 CS에서 빠져나오게 되면 lock을 해제하는 동시에 동기화 신호를 보내는 것이다. 동기화 신호는 다음 프로세스에게 CS을 사용해도 좋다는 신호를 주는 것이다. <br>

Critical Section 문제를 해결하기 위해서는 아래 세 가지 요구 조건을 충족시켜야 한다. <br>

1. 상호 배제(Mutual Exclusion): Critical Section에 프로세스가 있다면, 다른 프로세스의 진입을 금지한다. 

2. 진행(Progress): Critical Section을 사용하고 있지 않다면 다른 프로세스가 접근할 수 있도록 한다. 이때, 나머지 구역(Remainder Section)에서 실행 중이지 않은 프로세스들만 다음에 누가 해당 임계 구역으로 진입할 수 있는지를 결정하는 데 참여할 수 있으며, 이 선택은 무제한으로 연기될 수 없다.

3. 한정된 대기(Bounded Waiting): 프로세스가 Critical Section에 진입하려는 요청을 한 후부터 그 요청이 허용될 때까지 다른 프로세스들이 Critical Section에 진입하는 횟수에 한계가 있어야 한다.

## Synchronization Algorithms
### Algorithm 1
현재 CS에 들어갈 프로세스가 어떤 프로세스인지를 한 변수로 나타내어 일치하는 프로세스만 진입하도록 하는 단순한 방식이다. <br>

<img width="653" height="435" alt="Image" src="https://github.com/user-attachments/assets/a546fceb-9f1d-4e0d-a273-288a0b5a2cb8" />

이 방식은 Mutual Exclusion은 만족하지만 Progress에 만족하지 못한다. P_i가 CS에 진입하기 전에 죽어버리거나 한 Process가 두 번 연속 CS에 진입하지 못하는 경우에는 CS에 아무런 프로세스가 존재하지 않게 된다.

### Algorithm 2
특정 프로세스가 CS에 진입할 준비가 되었다는 것을 나타내는 변수를 두어, 다른 프로세스가 CS에 진입하려고 한다면 현재 프로세스는 기다리는 방법이다.

<img width="773" height="526" alt="Image" src="https://github.com/user-attachments/assets/567fb400-7587-4671-a303-e8285c5192cb" />

이 방식도 Mutual Exclusion은 만족하지만 Progress, Bounded Waiting에 만족하지 못한다. 두 프로세스가 flag=true를 수행하고 나면 두 프로세스 모두 무한히 CS에 진입하지 못하고 기다리는 상황이 발생하게 된다.

### Algorithm 3 (Peterson's Algorithm)
Peterson's Algorithm은 이전의 Algorithm 1과 2를 합쳐놓은 개념이다. turn과 flag 변수를 같이 사용한다.

<img width="474" height="397" alt="Image" src="https://github.com/user-attachments/assets/fbcd8e01-fbd7-46b7-9f05-b180874b4973" />

P_i 프로세스에 대해서, P_i는 flag[i] = true로 바꾸면서 CS에 진입하려고 한다. 그리고 turn = j로 바꿔주면서 상대방이 들어가게 한다. 만약 다른 프로세스가 들어가고 싶고 (flag[j] == true), 현재 상대방이 CS에 들어가 있으면 (turn == j)기다린다. 그렇지 않으면 P_i가 들어간다. CS에서 빠져나오면서 flag[i] = false로 바꿔준다. <br>

이 경우 Mutual Exclusion, Progress, Bounded waiting 모두 만족한다. 하지만, CS 진입을 기다리면서 계속 CPU와 메모리르 사용하는 Busy Waiting이 발생한다.

## Synchronization HW
하드웨어적으로 현재 상태를 확인하고 변경하는 Test & Modify를 Atomic하게 수행할 수 있도록 지원하면 CS 문제는 간단히 해결할 수 있다. 많은 시스템들은 이러한 하드웨어적 지원을 제공한다. <br>

이전까지의 알고리즘들은 데이터를 읽고 쓰는 것을 하나의 명령어로 처리할수 없기 때문에 복잡해졌다. 만약 메모리에서 데이터를 읽으면서 쓰는 것까지 하나의 명령어로 동시에 가능하다면 코드가 훨씬 간결해지고, 이는 Test_and_Set을 이용해서 아래와 같이 구현된다. <br>

<img width="579" height="670" alt="Image" src="https://github.com/user-attachments/assets/b330bc65-16df-4e6b-b8f9-e2a5f7fbc6fb" />

이러한 하드웨어적인 명령어는 Busy waiting과 Bounded Waiting 조건을 만족하지 못하는 단점이 있다.

## Semaphore
세마포어는 Busy Waiting이 필요없는 동기화 도구이며, 여러 프로세스나 스레드가 CS에 진입할 수 있는 Signaling 메커니즘이다. <br>

세마포어는 CS에 진입하기 전에 스위치를 사용 중으로 놓고 CS에 들어간다. 이후에 도착하는 프로세스는 앞의 프로세스가 작업을 마칠 때까지 기다린다. 프로세스가 작업을 마치면 세마포어는 다음 프로세스에 CS를 사용하라는 동기화 신호를 보낸다. <br>

세마포어는 다른 알고리즘과 달리 임계구역이 잠겼는지 직접 점검하거나 Busy Waiting을 하거나, 다른 프로세스에 동기화 메시지를 보낼 필요가 없다. <br>

<img width="1000" height="542" alt="Image" src="https://github.com/user-attachments/assets/e6ad67be-2e37-41b6-b850-19605f36b481" />

**P(S)는 공유 데이터를 획득하는 연산이고, V(S)는 반납하는 연산이다.** <br>

1. **Semaphore(n)**: 전역 변수 RS를 n으로 초기화한다. RS에는 현재 사용 가능한 자원의 수가 저장된다.
2. **P()**: 잠금을 수행하는 코드로 RS가 0보다 크면(사용 가능한 자원이 있다면) 1만큼 감소시키고 CS에 진입한다. 만약 RS가 0보다 작으면(사용 가능한 자원이 없다면) 0보다 커질 때까지 기다린다.
3. **V()**: 잠금 해제와 동기화를 같이 수행하는 코드로, RS 값을 1 증가시키고 사마포어에서 기다리는 프로세스에 CS에 진입해도 좋다는 `wake_up` 신호를 보낸다.

세마포어에서 잠금이 해제되기를 기다리는 프로세스는 큐에 저장되어 있다가 `wake_up` 신호를 받으면 큐에서 나와 CS에 진입한다. 따라서 Busy Waiting하는 프로세스가 없게 된다. <br>

그러나 세마포어의 `P()`, `V()` 내부 코드가 실행되는 도중에 context switching이 발생하면 Mutual Exclusion과 Bounded Waiting 조건을 보장하지 못한다. 따라서  `P()`, `V()`의 내부 코드는 검사와 지정을 사용하여 분리 실행되지 않고 완전히 실행되게 해야 한다. 즉, atomicity가 보장되어야 한다.


## Mutex
뮤텍스는 세마포어의 공유 자원(RS)가 1일 때를 말한다. 즉, 세마포어는 뮤텍스의 특별한 버전으로 RS가 1 이상일 때를 말한다. 따라서, 뮤텍스와 세마포어는 구동 방법, 원리가 모두 같다. <br>

```
wait(mutex);
// critical section
signal(mutex);
```

세마포어가 `P()`,`V()` 연산으로 이루어져 있다면, 뮤텍스는 `wait(mutex)`, `signal(mutex)`로 이루어져 있다. 이름만 다를 뿐이지 내부 연산은 같으므로 사실 이름은 크게 중요하지 않다. 즉, `wait`을 하면 공유 자원 mutex(이전에는 RS)를 하나 감소시키고, `signal`을 하면 mutex를 하나 증가시키고 block 상태에 빠져있는 프로세스를 뮤텍스 큐에서 깨워 ready queue로 보내는 역할을 한다. 따라서 뮤텍스 역시 세마포어와 같이 3가지 CS 조건인 Mutual Exclusion, Bounded Waiting, Progress를 지키면, Busy Waiting을 하지 않는 효율적인 알고리즘이다.

<img width="1000" height="775" alt="Image" src="https://github.com/user-attachments/assets/f1418815-ce61-46ef-b1ef-20c2ea46ae95" />

다음과 같이 mutex는 공유 자원이 하나일 때를 말한다.

1. 프로세스 P1이 먼저 wait(mutex)을 호출하여 mutex = 0으로 만들고 임계 구역에 진입한다.
2. 프로세스 P2가 wait(mutex)을 호출하지만 mutex는 이미 0이므로 임계 구역에 진입하지 못하고 block된다. mutex queue에 들어간다.
3. 프로세스 P3가 wait(mutex)을 호출하지만 mutex는 이미 0이므로 임계 구역에 진입하지 못하고 block된다. mutex queue에 들어간다.
4. 프로세스 P1이 임계구역의 일을 마치고 signal(mutex)을 호출하여 mutex = 1로 만들고 mutex queue에서 block 상태인 프로세스 P2를 깨운다.
5. 프로세스 P2는 ready queue에 들어가고 다시 wait(mutex)을 호출하고 mutex = 0으로 만들고 임계 구역에 진입한다.
6. 프로세스 P2이 임계구역의 일을 마치고 signal(mutex)을 호출하여 mutex = 1로 만들고 mutex queue에서 block 상태인 프로세스 P3를 깨운다.
7. 프로세스 P3는 ready queue에 들어가고 다시 wait(mutex)을 호출하고 mutex = 0으로 만들고 임계 구역에 진입한다.

세마포어는 mutex의 특별한 버전으로 공유자원이 n개 일 때(n >= 1)를 말하는 것이라고 볼 수 있다.

* * *

**동시성** <br>
https://spacebike.tistory.com/22 <br>