# 1. 폰 노이만 구조

초기 컴퓨터는 새로운 계산을 하려면 전선을 재배치하고 스위치를 조작하여 하드웨어를 변경해야 했다. <br>
그래서 폰 노이만이 프로그램 내장 방식(Stored Program Concept)을 제안했고, 이것이 현대 컴퓨터의 구조가 되었다. <br>

<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/eb7f013e-f987-48e8-a11a-26615bfee730"/>

- 컴퓨터에서 다른 작업을 진행할 때 하드웨어의 재배치 없이 소프트웨어만 변경하면 된다. (범용성 향상)
- 컴퓨터는 CPU, 메모리, 버스, 입출력 장치로 구성된다.
- 명령어(Instruction)와 데이터(Data)가 같은 메모리 공간에 저장되며, 같은 버스를 통해 CPU로 전달된다.
- fetch -> decode -> excute -> store 사이클로 명령어를 처리한다.

## 1.1. 폰 노이만 구조 단점
프로그램 메모리와 데이터 메모리가 하나의 버스를 공유하기 때문에 병목 현상(bottleneck)이 발생한다. <br>
즉, CPU가 아무리 빨라도 메모리에서 데이터를 가져오는 속도(전송 속도)가 느리면 전체 시스템 성능이 저하되는 것이다. <br>
(기억장치의 속도가 전체 시스템의 속도를 결정)

---

# 2. 메모리 계층 구조

Memory Hierachy는 컴퓨터의 모든 부품을 빠르고 저장 용량이 큰 하드웨어로 setting하면 좋겠지만, 용량, 접근 속도, 비용간의 절충 관계를 파악해 필요에 따라 채택할 수 있게 나타낸 구조이다. <br>

<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/b79a4f97-ea7e-4bbe-9fdc-1e7bd1633989" />

이미지를 확인해보면 위로 올라갈수록 bit당 cost가 높아지고, 내려갈수록 용량과 접근 시간이 늘어난다. <br>

## 2.1. Register
CPU 안에 있는 작은 메모리로 속도가 가장 빠르지만, 기억 용량이 적고 휘발성이다. <br>
ex) PC, IR, MAR...etc

## 2.2. Cache Memory
CPU와 Main Memory 사이에 존재하며, L1, L2, L3 cache가 존재한다.

- L1 Cache: CPU core 내부에 존재하며, 가장 빠른 캐시이다.
- L2 Cache: CPU 코어 내부/인접하게 존재한다.
- L3 Cache: CPU 내부에 존재하며, 멀티 코어 CPU에서 여러 코어가 공유하는 캐시이다.

### 2.2.3. Locality
캐시는 Locality(지역성)라는 성질을 사용해 동작한다. <br>

- Temporal Locality(시간 지역성): 한 번 참조된 데이터는 조만간 다시 참조될 가능성이 높다.
- Spatial Locality(공간 지역성): 참조된 데이터의 주변 데이터가 조만간 참조될 가능성이 높다.

이런 지역성을 사용해 캐시에 data를 담아두는 것이다.

### 2.2.3. Cache Hit / Miss

CPU에서 요청한 data가 Main Memory까지 가서 찾아오지 않고, 캐시에서 찾아오는 것을 **Cache Hit**라고 하고, <br>
만약 요청한 data가 캐시에 존재하지 않다면, **Cache Miss**라고 한다.

<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/a54a29de-ac82-496e-9a85-a438be9553db" />

위 이미지를 확인해보면 캐시 미스가 발생해서 Main Memory까지 다녀오면 Access Time이 10배나 늘어날 수 있다. (25ns -> 250ns) <br>

그래서 코드를 작성할 때 캐시 친화적으로 작성해야하는 것이다. <br>
(자세한 블로그 https://velog.io/@piopiop/%ED%96%89%EB%A0%AC%EA%B3%B1%EC%85%88-%EC%B5%9C%EC%A0%81%ED%99%94-%EA%B3%B5%EA%B0%84-%EC%A7%80%EC%97%AD%EC%84%B1%EC%9D%84-%ED%99%9C%EC%9A%A9%ED%95%9C-%EC%BA%90%EC%8B%9C-%EC%B9%9C%ED%99%94%EC%A0%81-%EC%BD%94%EB%93%9C-%EC%9E%91%EC%84%B1)

# 3. CPU 구조








---

# 참고자료

## 폰노이만 구조
https://jiwondev.tistory.com/109 <br>
https://wikidocs.net/63816 <br>
https://m.blog.naver.com/with_msip/221981730449 <br>

## 메모리 계층 구조
https://www.geeksforgeeks.org/computer-organization-architecture/memory-hierarchy-design-and-its-characteristics/ <br>
https://nayoungs.tistory.com/entry/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B3%84%EC%B8%B5-%EA%B5%AC%EC%A1%B0Memory-Hierachy
