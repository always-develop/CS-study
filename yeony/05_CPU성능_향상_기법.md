# 05-1. 빠른 CPU를 위한 설계 기법

- CPU를 설계하는 엔지니어는 어떻게 하면 CPU를 빠르게 동작할 수 있는지 고민할 것이다
- 앞으로 그 어떻게에 대한 내용이 나온다

## 클럭

- 클럭의 박자에 맞춰 컴퓨터 부품들은 움직인다
- CPU는 명령어 사이클에 따라 명령어를 실행한다
- 클럭의 속도에 맞춰서 CPU가 명령어 사이클을 돌리기 때문에, 클럭의 속도가 빠르면 빠를 수록 CPU는 더 빠르게 일할 것이다.
- 이런 클럭의 속도의 단위는 `Hz(헤르츠)` 이다.
- 1초에 클럭이 한번 반복되면 1Hz, 1초에 100번이면 100Hz이다

<aside>
💡 클럭의 속도를 시계와 같이 생각하면 속도가 일정해보인다.
그러나 클럭의 속도는 일정하지 않고, 기본 클럭 속도(base)와 최대 클럭 속도(max)가 정해져있고, 고성능을 유지하면 속도를 높힌다.
클럭의 최대 속도보다 더 높이 끌어올리는 것을 `오버클럭킹`이라고 한다.

</aside>

- 무작정 클럭의 속도만 높인다면 컴퓨터 발열 현상이 심하게 나타난다
- CPU 성능을 높이는 다른 방법을 살펴보자

## 코어와 멀티코어

### 코어의 정의

- 명령어를 실행하는 부품 = 하나의 코어
- 앞서 우리가 배웠던 CPU는 `APU + 제어장치 + 레지스터` 로 이루어져 있다 하였다
- 저렇게 한 세트로 이루어진 부품을 1코어라고 부른다
- 명령어 실행을 하는 코어가 많은 수록 명령어를 처리하는 일꾼이 많아서 더 빠른 일처리를 할 수 있다
- 그러나 일의 분배가 잘되지 않으면 그만큼 효율이 나지 않을수도 있고, 처리할 일은 적은데 오히려 일꾼이 많으면 효율적이라고 할 수는 없다
- 그래서 무조건적으로 코어가 많다고 하여 CPU 성능이 좋다고 할 수도 없다

## 스레드와 멀티스레드

### 스레드의 정의

- 실행 흐름의 단위
- `하드웨어적 스레드`
  - 하나의 코어가 동시에 처리하는 명령어 단위
  - 하지만 하나의 코어가 하나의 명령어만 실행할 수 있는건 아니다
  - 예를 들어, `2코어 4스레드` 는 코어는 2개, 스레드는 4개로 한 번에 4개의 명령어를 처리할 수 있다
  - 이런식으로 하나의 코어로 여러개의 명령어를 동시에 처리하는 CPU를 `멀티스레드 프로세서`, `멀티스레드 CPU`라고 한다
- `소프트웨어적 스레드`
  - 하나의 프로그램에서 독립적으로 실행되는 단위
  - 프로그램의 여러 부분이 동시에 실행될 수도 있다
    - 이 기능을 위한 코드를 각각의 스레드로 만들면 동시에 실행할 수 있다
  - 예를 들어 워드프로세서를 개발한다면
    - 입력받은 내용을 화면에 보여주기
    - 입력한 내용이 맞춤법에 맞는지 검사하기
    - 입력한 내용을 스스로 저장하기
  - 위의 기능 세개를 동시에 실행해야한다는 말이다
- 소프트웨어적 스레드 관점에서 생각하면 1코어 1스레드 CPU도 여러개의 명령어를 실행할 수 있다
- `멀티스레드 프로세서`
  - 하나의 코어로 여러 명령어를 동시에 처리하도록 만드려면 `레지스터`가 핵심이다
    - 프로그램 카운터, 스택 포이터, 데이터 버퍼 레지스터, 데이터 주소 레지스터 등
  - 이렇게 하나의 명령어를 처리하기 위한 레지스터 세트를 여러개 가지고 있으면 된다
- `논리 프로세서`
  - 2코어 4스레드 CPU가 네 개의 명령어를 처리하면 프로그램 입장에서는 한 번에 하나의 명령어를 처리하는 CPU가 4개가 있는 것 같다
  - 그래서 하드웨어 스레드를 논리 프로세서라고 부르기도 한다

# 05-2. 명령어 병렬 처리 기법

- 성능 좋은 클럭과 멀티 스레드 CPU를 사용하면서 동시에 CPU가 효율적으로 명령어를 처리하게 만드는 것도 중요하다
- 대표적으로 `명령어 병렬 처리 기법`이 있다

## 명령어 파이프라인

- 명령어 처리 과정을 클럭 단위로 나누면 아래와 같다
  - 명령어 인출
  - 명령어 해석
  - 명령어 실행
  - 결과 저장
- CPU는 같은 단계를 동시에 실행할 수는 없지만, 다른 단계라면 동시에 실행할 수 있다
  - 예시)명령어 1의 해석하면서 동시에 명령어 2의 인출을 할 수 있다
- 이런식으로 명령어들을 `명령어 파이프라인`에 넣고, 동시에 실행하는 것을 `명령어 파이프라이닝`이라고 한다
- 이런 기법은 높은 효율을 가져오지만 특정 상황에서는 위험도 있다

### 데이터 위험

- 명령어 간 데이터 의존성에 의해 발생한다
- B명령어 실행 결과를 A명령어에서 사용해야 한다면 A명령어는 B명령어의 데이터에 의존적이라고 말한다
- 이런 의존적인 관계를 가진 명령어를 동시에 실행하는 것은 파이프라인이 제대로 작동하지 않을 것이다

### 제어 위험

- 분기 등으로 인한 프로그램 카운터의 갑작스러운 변화에 의해 발생한다
- 프로그램의 실행 흐름이 갑자기 바뀌면 미리 가지고 와서 처리 중이던 명령어들은 쓸모가 없어진다
- 이를 방지하기 위해 분기 예측 기술을 이용해 어디로 분기할지 미리 예측한다

### 구조적 위험

- 명령어들이 동시에 실행되고 있을 때, 같은 CPU 부품을 사용하려고 할 때 발생한다
- 자원 위험이라고도 한다

## 슈퍼스칼라

- CPU 내부에 여러 개의 파이프라인을 포함한 구조를 `슈퍼스칼라`라고 한다
  - 슈퍼스칼라 구조로 명령어 처리가 가능한 CPU를 `슈퍼스칼라 프로세서`, `슈퍼스칼라 CPU`라고 부른다
- 파이프라인이 여러 개면 동시에 실행할 수 있는 명령어가 더 많아진다
- 그렇기 때문에 위에서 나온 위험들에 더 많이 노출될 수 있기 때문에 고도의 설계가 필요하다

## 비순차적 명령어 처리

- 명령어들을 순차적으로 실행하지 않는 기법
  - 새치기.. ?
- 순차적으로 실행되고 있던 명령어가 예상치 못한 상황에서 처리되지 못한다면 파이프라인이 멈춰버린다
- 즉, 의존성을 가진 명령어를 처리하기 위해 먼저 처리되는 명령어들과 아무런 관계가 없는 명령어들이 기다리는 것은 비효율적이다
- 의존성이 없는 명령어들의 처리 순서를 앞으로 옮겨서 최대한 짧은 시간 내에 효율적으로 명령어 처리를 하기 위해 사용하는 방법이다
  - 아무거나 바꿀 수는 없고, 의존성이 있는지 없는지를 잘 판단하여 순서를 바꿔야 한다

# 05-3. CISC와 RISC

- 파이프라이닝 하기 쉬운 명령어는 뭘까?
- 명령어가 어떻게 생겨야 파이프라이닝하기 쉬울까?

## 명령어 집합

- 수많은 CPU 제조사가 있고, 다양한 규격의 CPU가 존재하는데 CPU가 이해하고 실행하는 명령어는 다 똑같이 생겼을까?
  - CPU의 큰 틀은 동일하지만 세세하게 보면 조금씩 다르다
- CPU가 이해할 수 있는 명령어들의 모음을 `명령어 집합`이라 하고, 같은 말로 `명령어 집합 구조(ISA, Instruction Set Architecture)`이라 한다
- ISA가 다른 CPU는 서로의 명령어를 이해할 수 없다
  - ISA가 다르면 어셈블리어도 달라진다
- 즉 ISA는 CPU의 언어라고 이해할 수 있고, ISA는 하드웨어가 소프트웨어를 어떻게 이해할지에 대한 약속이기도 하다
- 명령어 병렬 처리 기법을 사용하기에 유리한 명령어 집합도 있고, 아닌 명령어 집합도 있을 것이다
- 앞으로 병령 처리 기법을 사용하기에 유리한 대표적인 ISA를 소개한다

## CISC : Complex Instruction Set Computer

- 복잡하고, 다양한 명령어들을 활용하는 CPU 설계 방식
  - ex\_ intel의 x86, x86-64
- 가변 길이 명령어 집합을 활용한다
- 적은 수의 명령어로도 프로그램을 동작시킬 수 있다.
  - ARM보다 짧은 명령어 사용이 가능하다
- 명령어가 복잡하기 때문에
  - 실행되는 시간이 일정하지 않다
  - 명령어 하나를 실행하는데 여러 클럭 주기를 필요로 한다
    - 하나의 명령어가 많은 것을 담당하기 때문
- 명령어 파이프라인은 일정한 시간을 소요하며 규칙적으로 실행되어야 가장 이상적이다
  - 공장처럼 움직이기 때문에,, 가급적 1클럭이 적절하다고 한다
- 따라서 명령어가 규격화되어 있지 않기 때문에 명령어 파이프라인의 효율이 떨어진다
  - 그리고 나중에 알고보니, 쓰던 명령어만 많이 쓰고, 복잡한 명령어는 잘 안쓰더라..
- 이런 CISC 설계 방법은 파이프라인의 효율을 살리지 못해 CPU를 효율적으로 설계하기에 한계가 있다

## RISC : Reduced Instruction Set Computer

- 명령어의 길이가 짧고(`고정 길이 명령어`), 규격화되어 있고, 속도 또한 1클럭을 지향한다
  - CISC의 단점들을 보완했다
  - ex\_ ARM
- 파이프라이닝에 최적화 되어 있는 설계 방법이다
- 메모리 접근하는 명령어를 `load`와 `store` 2가지로 제한하여 최대한 단순한 명령어를 지향한다
  - 그 대신 레지스터 접근을 많이 활용한다
  - 그래서 레지스터를 이용한 연산이 많고, 레지스터의 개수도 CISC보다 많다
