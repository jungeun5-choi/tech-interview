<details>
<summary> <h3> Q. Docker에 대해서 설명해보시오. (Docker와 Docker Compose 및 Swarm, K8S의 구분) </h3></summary>

<br>

- <b>Docker:</b> 컨테이너 기반 오픈소스 가상화 플랫폼

- <b>컨테이너:</b> 격리된 공간에서 프로세스를 동작하는 기술 (= 프로세스 격리).<br>
추가적인 OS(= 게스트 OS)를 설치하여 가상화하는 방법은 성능에 문제가 있었고, 프로세스를 격리하는 방식이 등장했는데, 그게 컨테이너 방식임.

- <b>Docker Compose:</b> Docker의 확장 기능으로, <u>다중 컨테이너 애플리케이션을 정의하고 배포</u> 가능.<br>
YAML 파일을 사용하여 서비스, 네트워크, 볼륨 등을 선언적으로 구성

- <b>Docker Swarm:</b> Docker 기반의 <u>클러스터링 솔루션</u>.<br>
여러 Docker 호스트를 하나의 가상 Docker 호스트로 관리할 수 있다.<br>
자동 로드 밸런싱 / 서비스 디스커버리 / 스케일링 등

- <b>Kubernetes:</b> 컨테이너 오케스트레이션 도구, Docker 생태계와 상호 보완적으로 사용. <br>
Docker Swarm보다 편리한 관리를 제공

</details>

<br>

<details>
<summary> <h3> Q. Docker vs Kubernetes 비교 </h3></summary>

<br>

|  | Docker | Kubernetes |
| --- | --- | --- |
| <b>기능 및 역할</b> | 컨테이너 생성, 실행, 관리 등의 기능을 제공 | 컨테이너화 된 애플리케이션 배포/스케일링/관리 등을 자동화하는 오케스트레이션 도구 |
| <b>범위</b> | 단일 호스트 내에서 클러스터 관리 | 여러 호스트에 걸친 컨테이너 클러스터 관리 |
| <b>주요 기능<b> | 컨테이너 이미지 빌드, 컨테이너 생성/시작/중지, 네트워크 및 볼륨 관리 등 | 오토스케일링 / 로드 밸런싱 / 서비스 디스커버리 / 롤링 업데이트 / 헬스 체크 등 |
| <b>아키텍처</b> | 단일 호스트 기반의 단순한 아키텍처 | 마스터-노드 구조의 분산 아키텍처 – 고가용성과 확장성 제공 |
| <b>배포 모델</b> | 단일 호스트 내에서 애플리케이션 배포 | 클러스터 내 여러 노드에 걸친 애플리케이션 배포 및 관리 |

</details>

<br>

<details>
<summary> <h3> Q. 리눅스의 네임스페이스란 무엇인가? </h3> </summary>

<br>

#### 네임스페이스:
프로세스 간에 시스템 리소스를 격리하는 역할.<br>
각 프로세스는 자신만의 namespace를 가지게 됩니다. (격리는 커널이 한다)<br>
대표적인 namespace는 PID, Mount, Network, UTS, IPC, User 등.<br>
프로세스는 다른 namespace의 리소스를 볼 수 없다.

#### cgroups: 
= control groups.<br>
프로세스 그룹에 대한 리소스를 제한하고 격리한다.<br>
(예를 들면, CPU, 메모리, 디스크 I/O, 네트워크 대역폭 등)<br>
시스템 전체의 리소스를 효율적으로 관리할 수 있다.

</details>

<br>

<details>
<summary> <h3> Q. 리눅스의 네임스페이스와 컨테이너 간의 관계? </h3> </summary>

<br>

1. <b>Docker와 Kubernetes 등의 컨테이너 기술은 namespace와 cgroups를 활용하여 컨테이너를 구현.</b> <br>
namespace와 cgroups 기능을 활용하여 애플리케이션의 격리/보안/리소스 관리 등을 제공한다.

2. 각 컨테이너는 자신만의 namespace를 갖고 있다. <br>
<u>= 즉, 호스트 시스템의 리소스와 격리된다.</u>

3. cgroups를 사용해, 컨테이너 별로 리소스 사용을 제한할 수 있다.

4. 이를 통해 컨테이너는 서로 독립적으로 실행되며, <br>
리소스 경합 없이 안정적으로 동작할 수 있게 된다.

</details>

<br>

<details>
<summary> <h3> Q. 보통 컨테이너에 설치된 환경이 베어메탈에 설치된 환경보다 안전하다고 이야기하는데 왜 그런 이야기가 나올까? </h3> </summary>

<br>

1. <b>격리성:</b> 각 컨테이너는 자체적인 파일 시스템, 네트워크, 프로세스 등을 가지고 있어 서로 격리되어 있다. (즉, 서로 영향을 미치지 않는다.)

2. <b>최소 권한 원칙:</b> 컨테이너는 최소한의 권한만을 가지고 실행되므로, 호스트 시스템에 대한 접근이 제한된다.

3. <b>불변성:</b> 컨테이너 이미지는 변경이 어려운 불변 상태로 유지된다. = 악성 코드 삽입, 설정 변경 방지

</details>

<br>

<details>
<summary> <h3> Q. Docker와 하이퍼바이저 기반 가상화의 차이점에 대해서 설명하시오. </h3> </summary>

<br>

Docker는 Type2 하이퍼바이저처럼 OS 위에서 컨테이너 엔진을 실행하는데요<br>
차이점이 있다면 게스트 운영체제 없이 애플리케이션을 실행시킵니다.<br><br>
컨테이너 내부에서 애플리케이션 이미지를 실행하기 때문에<br>
어떤 운영체제 환경에서도 동일하게 실행시킬 수 있다는 특징이 있습니다.


</details>