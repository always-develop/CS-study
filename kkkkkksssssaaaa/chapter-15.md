# 15장. 파일 시스템

# [CS] 👽 혼자 공부하는 컴퓨터구조+운영체제

---

## 15장. 파일 시스템

### 15-1. 파일과 디렉터리

- 파일은 보조기억장치에 저장된 정보의 집합의 논리적인 단위를 의미한다
- 모든 파일에는 파일을 실행하기 위한 정보와 부가 정보들이 있다
  - 이 정보들을 `속성(Attribute)` 또는 `메타데이터(Metadata)` 라고 한다
- 파일을 다루는 모든 작업들은 운영체제가 수행한다
  - 운영체제는 파일 연산을 위한 `System call` 을 제공한다고 한다
- 파일을 관리하기 위해 디렉터리 혹은 폴더라는 집합으로 관리하며 트리 구조의 형태를 띈다
  - 트리 구조의 최상위 디렉터리를 루트 디렉터리라고 부르며 `/` 로 표기한다
  - 트리 구조에서 특정 디렉터리를 찾기 위한 `경로` 가 존재하는데, 루트 디렉터리부터 자신에게 이르는 경로를 `절대 경로`, 특정한 디렉터리부터 시작하는 경로를 `상대 경로` 라고 표현한다
- 디렉터리도 파일이다
  - 파일이 파일과 관련된 정보를 담고 있다면 디렉터리는 내부에 담긴 파일과 관련된 정보를 담고 있으며 테이블 형태로 구성된다

### 15-2. 파일 시스템

- 보조기억장치를 사용하기 위해서는 우선 `파티셔닝` 과 `포맷` 을 거쳐야 한다
- `파티셔닝(Partitioning)` 이란?
  - 저장 장치의 논리적인 영역을 구획하는 작업이다
  - 나뉘어진 영역 하나 하나를 `파티션(Partition)` 이라고 한다
- `포매팅(Formatting)` 이란?
  - 저장 장치의 데이터를 초기화 하는 작업이라고 알고 있겠지만… 정확한 표현은 아니라고 한다!
  - 정확하게는 파일 시스템을 설정하여 어떤 방식으로 파일을 저장하고 관리할 것인지 결정하고, 새 데이터를 쓸 준비를 하는 작업을 의미한다고 한다
    - 데이터 초기화가 포함되어 있기는 하다
  - 어떤 파일 시스템으로 디스크의 파일을 관리할 것인지는 포맷 단계에서 결정된다
- 운영체제는 파일과 디렉터리를 `블록(Block)` 이라는 단위로 읽고 쓴다
  - 하드 디스크의 가장 작은 저장단위는 섹터이지만, 운영체제는 하나 이상의 섹터를 블록이라는 단위로 묶은 뒤, 블록 단위로 파일과 디렉터리를 관리한다
  - 파일 시스템이 모든 섹터를 관리하기에는 개수가 너무 많고 크기도 작기 때문이라고 한다
- 크기가 큰 파일은 여러 블록에 걸쳐 저장 되는데, 이 때에도 데이터를 어떻게 할당할 것인지에 대한 방식이 여러 개 존재한다
  - `연속 할당`
    - 말 그대로 연속된 블록에 저장하는 방식
    - 이 방식도 외부 단편화를 야기할 수 있다
  - `불연속 할당`
    - `연결 할당`
      - 연결 리스트처럼 블록 내부에 다음 블록을 가리키는 정보를 가지고 있어, 논리적으로 연결하여 저장하는 방식
      - 연결 리스트처럼 탐색 성능이 안좋다는 단점이 있다
        - 중간 블록부터 접근하고 싶어도 무조건 첫 번째 블록부터 순서대로 접근해야 한다고 한다
        - 특정 블록에 문제가 있다면 다음 블록부터는 접근할 수 없다
    - `색인 할당`
      - 파일의 모든 블록 주소를 `색인 블록` 이라는 하나의 블록에 모아 관리하는 방식이라고 한다
- `FAT 파일 시스템`
  - 주로 USB 메모리, SD 카드 등의 저용량 저장 장치에서 사용된다고 한다
  - 연결 할당 방식을 보완했다고 한다
    - 연결 할당 방식의 근본적인 원인은 블록 안에 다음 블록 주소를 저장한 것이었는데, 이 점을 보완했다
  - 다음 블록에 대한 주소를 한데 모아 테이블 형태로 관리하는 방식이 `FAT(File Allocation Table)` 이라고 한다
  - MS-DOS 에서 사용되었다고 한다
  - 블록을 표현하는 비트 수에 따라 FAT12, FAT32 등등으로 구분한다
- `유닉스 파일 시스템`
  - 색인 할당을 기반으로 하며, 색인 블록을 `i-node(Index-Node)` 라고 표현한다
  - 파일마다 i-node 가 있고, 각자 번호가 부여되어 있으며, 열 다섯개의 블록 주소룰 저장할 수 있으며, 파티션 내 특정 영역에 모여있다고 한다
  - 다만, 열 다섯개의 블록 주소만 가리킬 수 있기 때문에, 블록 개수가 많을 때에 대한 대책이 필요하다
    - 12번 까지는 실제 파일의 데이터를 저장하는 `직접 블록(Direct Block)` 으로 다루고
    - 13~15번에는 간접 블록을 저장한다
      - 포인터처럼, 파일 블록을 저장하고 있는 다른 파일 블록을 참조하는 것이다
      - 참조의 depth 에 따라 단일 간접 블록, 이중 간접 블록, 삼중 간접 블록으로 나뉜다
- 이 외에도 다양한 파일 시스템이 있다
  - 주로 윈도우에서 쓰는 `NT 파일 시스템`, 리눅스에서 사용되는 `ext 파일 시스템` 이 있다
- 작업 중 시스템에 손상이 가서 파일 시스템이 손상될 때(`시스템 크래시`)를 대비하여 `저널링(Journaling)` 기법을 사용한 `저널링 파일 시스템` 이라는 것도 있다
  - 작업 직전에 파티션의 로그 영역에 변경사항에 대한 로그를 남기고
  - 로그를 남긴 후 작업을 수행하며
  - 작업 완료 후 로그를 삭제한다
  - 즉, 시스템 크래시가 발생한 경우 로그만 확인하는 방식으로 시스템을 복구할 수 있게 된다고 한다
  - 대부분의 파일 시스템은 저널링 기능을 지원한다고 한다
- `마운트(Mount)` 란?
  - 유닉스 계열 운영체제에서 볼 수 있는 단어
  - 한 저장 장치의 파일 시스템에서 다른 저장 장치의 파일 시스템에 접근할 수 있도록 파일 시스템을 편입시키는 작업을 의미한다
