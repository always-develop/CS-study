# 01. 컴퓨터 구조 시작하기

# [CS] 👽 혼자 공부하는 컴퓨터구조+운영체제

---

## 01. 컴퓨터 구조 시작하기

### 01-1. 컴퓨터 구조를 알아야 하는 이유

- 개발자로써 컴퓨터 구조를 알아야 하는 이유는… 서버 컴퓨터를 정해야할 때, 적절한 사양의 컴퓨터를 선택할 수 있어야 하기 때문..
  - 성능, 용량, 비용의 문제는 코딩 잘한다고 알 수 있는게 아니다

### 01-2. 컴퓨터 구조의 큰 그림

- 컴퓨터가 이해하는 정보는 `데이터` 와 `명령어` 가 있다
- 명령어는 컴퓨터를 작동시키는 정보이고, 데이터는 명령을 위해 존재하는 재료이다
- 메모리라는 곳에 저장된 데이터에 접근하려면, 마치 현실에서 주소를 통해 원하는 위치를 찾아가듯, 메모리 `주소` 를 통해 원하는 데이터에 접근할 수 있다
- CPU 의 구성 요소
  - 산술 논리 연산 장치(Arithmetic Logic Unit, ALU)
    - 계산기같은 녀석
  - 레지스터(Register)
    - 임시 데이터 저장 장치
  - 제어 장치(Control Unit)
    - 제어 신호라고 하는 전기 신호를 내보내고 명령어를 해석하는 장치
- 메모리는 실행 중인 프로그램의 정보를 저장하고, 보조기억장치는 영구적으로 보관할 프로그램을 저장한다
- 메인보드에 연결된 부품들은 `버스` 라는 데이터 통로를 통해 정보를 주고받는다
  - 그 중, `시스템 버스` 는 컴퓨터의 핵심 부품인 CPU, 메모리, 보조기억장치, 입출력장치를 연결하는 가장 중요한 버스이다
- 시스템 버스는 `주소 버스`, `데이터 버스`, `제어 버스` 로 이루어져있다
  - `주소 버스(Address Bus)` 란 주소를 주고받는 통로이다
  - `데이터 버스(Data Bus)` 란 명령어와 데이터를 주고받는 통로이다
  - `제어 버스(Control Bus)` 란 제어 신호를 주고받는 통로이다
- CPU 가 메모리를 읽을 때
  - CPU 는 제어 버스로 메모리 읽기 신호를 보내면서
  - 주소 버스로 읽고자 하는 메모리 주소를 내보내면
  - 메모리는 데이터 버스를 통해 요청한 주소에 있는 데이터를 CPU 에게 보낸다
- CPU 가 메모리에 쓸 때
  - 제어 버스를 통해 메모리 쓰기 제어 신호를 보내면서
  - 데이터 버스를 통해 메모리에 저장할 값과
  - 주소 버스를 통해 데이터를 저장할 주소를 보낸다

### 마무리
