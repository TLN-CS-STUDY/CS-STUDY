# Address Space and Dynamic Relocation

초기엔 하나의 프로그램이 전체 메모리를 독점했지만 <br>
time-sharing으로 인해 여러 프로세스가 동시에 메모리에 올라가야하는 문제와 함께 아래의 문제가 발생했다.

- Isolation: 프로세스는 다른 프로세스의 메모리를 건드리면 안된다.

- Efficiency: 각 프로그램이 메모리 어디에 위치할지 고민하지 않고, 마치 자기가 메모리 전체를 다 쓰는 것처럼 착각하게 만들어줘야 개발이 편해짐

## Address Space Abstraction

Efficiency를 위해 OS는 프로세스에게 0번지부터 max번지까지의 주소 공간을 가지고 있다. 는 것처럼 인식하게 해준다. <br>
그리고 이를 Address Space라고 부르며, 아래와 같이 나누어져 있다.

- **Code**: 기계어 명령어들이 저장되는 곳

- **Heap**: 개발자가 malloc이나 new로 동적 할당하는 공간

- **Stack**: 지역 변수, 함수 리턴 주소 등이 저장되는 공간

<img width="422" height="251" alt="image" src="https://github.com/user-attachments/assets/1ed47508-c9e6-41c7-9602-683f0e11243a" />

## Base and Bound

그러면 프로세스가 추상화된 메모리 주소를 사용하려하면, 이를 실제 memory address로 변경해줘야하고, <br>
이를 Dynamic Relocation이라고 한다.

<img width="419" height="191" alt="image" src="https://github.com/user-attachments/assets/1342641c-71ce-4aa8-a302-9b2e82f483a0" />
<img width="635" height="251" alt="image" src="https://github.com/user-attachments/assets/96d3baaa-db41-4bd3-9946-14b82ab81da7" />


> 그리고 여기서 잘못된 주소가 나오는 상황 즉, bound를 넘어가는 상황을
> Segmentation Fault 라고 한다.

하지만 base-bound 방식에도 한계가 존재하고 이를 보완하기 위해 Segmentation을 사용한다.

<img width="203" height="335" alt="image" src="https://github.com/user-attachments/assets/a112cd30-e4c9-444d-939c-70765e8c3ee3" />


- internal fragmentation
- the number of processes afforted in
- physical memory space
  - runtime cost of write-back at context-switching

---

# Segmentation

Internal fragmentation problem 해결과 Redundant data를 위해 나온 방법으로 <br>
주소 공간을 논리적 단위인 Segment로 쪼개서, 필요한 부분만 따로 메모리에 올리는 방법이다.
