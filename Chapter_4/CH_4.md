## 4.1 개요 Overview
스레드는 CPU이용의 기본 단위이다. 스레드는 스레드 ID, 프로그램 카운터(PC), 레지스터 집합과 스택으로 구성된다. 스레드는 같은 프로세스에 속한 다른 스레드와 코드, 데이터, 열린 파일이나 신호와 같은 운영체제 자원들을 공유한다.
<br>

- **동기 Motivation**
	다중 스레드 응용 프로그램의 몇 가지 예시
	- 이미지 모음에서 사진 축소판을 만드는 응용 프로그램은 별도의 스레드를 사용하여 개별 이미지에서 축소판을 생성할 수 있다.
	- 웹 브라우저는 하나의 스레드가 이미지 또는 텍스트를 표시하고 다른 스레드는 네트워크에서 데이터를 검색하도록 할 수 있다.
	- 워드 프로세서에는 그래픽을 표시하는 스레드, 사용자의 키 입력에 응답하는 또 다른 스레드 및 백그라운드에서 맞춤법 및 문법 검사를 수행하는 세 번째 스레드가 있을 수 있다.
<br>

- **다중 스레드 프로그래밍의 이점**
	1. **응답성(responsiveness)**: 대화형 응용을 다중 스레드화하면 응용 프로그램의 일부분이 봉쇄되거나, 응용 프로그램이 긴 작업을 수행하더라도 프로그램의 수행이 계속되는 것을 허용함으로써, 사용자에 대한 응답성을 증가시킨다.
	2. **자원 공유(resource sharing)**: 프로세스는 공유 메모리와 메시지 전달 기법을 통하여만 자원을 공유할 수 있다. 스레드는 반면에 자동으로 그들이 속한 프로세스의 자원들과 메모리를 공유한다. 코드와 데이터 공유의 이점은 한 응용 프로그램이 같은 주소 공간 내에 여러 개의 다른 작업을 하는 스레드를 가질 수 있다는 점이다.
	3. **경제성(economy)**: 프로세스 생성을 위해 메모리와 자원을 할당하는 것은 비용이 많이 든다. 스레드는 자신이 속한 프로세스의 자원들을 공유하기 때문에, 스레드를 생성하고 문맥 교환하는 것이 더욱더 경제적이다.
	4. **규모 적응성(scalability)**: 다중 스레드의 이점은 다중 처리기 구조에서 더욱 증가할 수 있다. 다중 처리기 구조에서는 각각의 스레드가 다른 처리기에서 병렬로 수행될 수 있기 때문이다.

## 4.2 다중 코어 프로그래밍 Multicore Programming
단일 컴퓨팅 칩에 여러 컴퓨팅 코어를 배치한 시스템을 다중 코어라고 한다. 여러 코어가 있는 시스템에서 병행성은 시스템이 각 코어에 별도의 스레드를 할당할 수 있기 때문에 일부 스레드가 병렬로 실행될 수 있다.

- **프로그래밍 도전과제 Programming Challenges**
	운영체제 설계자는 병렬 수행이 될 수 있도록 여러 코어를 활용하는 스케줄링 알고리즘을 개발해야 한다.
	> **_Amdahl's Law_**
	Amdahl's Law 는 순차 실행(병렬 실행이 아닌) 구성요소와 병렬 실행 구성요소로 이루어진 응용에 추가의 계산 코어를 더했을 때 얻을 수 있는 잠재적인 성능 이득을 나타내는 공식이다.

	일반적으로 다중 코어 시스템을 위해 프로그래밍하기 위해서는 5개의 극복해야 할 도전 과제가 있다.
	1. **테스크 인식(identifying tasks)**: 응용을 분석해 독립된 병행 가능 태스크로 나눌 수 있는 영역을 찾는 작업.
	2. **균형(balance)**: 찾아진 영역들이 전체 작업에 균등한 기여도를 가지도록 태스크를 나누는 작업.
	3. **데이터 분리(data spliting)**: 태스크가 접근하고 조작하는 데이터 또한 개별 코어에서 사용할 수 있도록 나누어져야 한다.
	4. **데이터 종속성(data dependency)**: 테스크가 접근하는 데이터는 둘 이상의 태스크 사이에 종속성이 없는지 검토되어야 한다.
	5. **시험 및 디버깅(testing and debugging)**: 프로그램이 다중 코어에서 병렬로 실행될 때, 다양한 실행 경로가 존재할 수 있다. 병행 프로그램을 시험 및 디버깅하는 것은 단일 스레드 응용과 비교하면 근본적으로 훨씬 어렵다.
<br>

- **병렬 실행의 유형 Types of Parallelism**
	- 데이터 병렬 실행: 동일한 데이터의 부분집합을 다수의 계산 코어에 분배한 뒤 각 코어에서 동일한 연산을 실행하는 데 초점을 맞추는 것.
	- 테스크 병렬 실행: 데이터가 아닌 태스크(스레드)를 다수의 코어에 분배한다. 각 스레드는 고유의 연산을 실행한다.

## 4.3 다중 스레드 모델 Multithreading Models
**사용자 스레드(user threads)** 와 **커널 스레드(kernel threads)**

- **다대일 모델 Many to One Model**
	많은 사용자 수준 스레드를 하나의 커널 스레드로 사상한다.
	한 스레드가 봉쇄형 시스템 콜을 할 경우 전체 프로세스가 봉쇄되고 하나의 스레드만이 커널에 접근할 수 있기 때문에 다중 스레드가 다중 코어 시스템에서 병렬로 실행될 수 없다는 단점이 있다.
<br>

- **일대일 모델 One to One Model**
	각 사용자 스레드를 각각 하나의 커널 스레드로 사상한다.
	다대일 모델보다 더 많은 병렬성을 제공한다. 그리고 다중 처리기에서 다중 스레드가 병렬로 수행되는 것을 허용한다.
	사용자 스레드 하나당 커널 스레드 하나를 만들어야 하며 많은 수의 커널 스레드가 시스템 성능에 부담을 줄 수 있다는 단점이 있다. Linux는 Windows 제품군과 함께 일대일 모델을 구현한다.
<br>

- **다대다 모델 Many to Many Model**
	여러 개의 사용자 수즌 스레드를 그보다 작거나 같은 수의 커널 스레드로 멀티플렉스 한다.
	다대다 모델은 위 두 가지의 모델의 단점을 어느정도 개선하였다. 개발자는 필요한 만큼 많은 사용자 수준 스레드를 생성할 수 있고 상응하는 커널 스레드가 다중 처리기에서 병렬로 수행될 수 있다. 또한, 스레드가 봉쇄형 시스템 콜을 발생시켰을 때 커널이 다른 스레드의 수행을 스케줄 할 수 있다.
	구현하기 어렵다. 또한 대부분의 시스템에서 처리 코어 수가 증가함에 따라 커널 스레드 수를 제한하는 것의 중요성이 줄어들었다.

## 4.4 스레드 라이브러리 Threads Library
스레드 라이브러리는 프로그래머에게 스레드를 생성하고 관리하기 위한 API를 제공한다.
스레드 라이브러리의 구현은 커널의 지원 없이 사용자 공간에서만 라이브러리를 제공하는 것과 운영체제에 의해 지원되는 커널 수준 라이브러리를 구현하는 것이다.
- 비동기 스레딩
	부모가 자식 스레드를 생성한 후 부모는 자신의 실행을 재개하여 부모와 자식 스레드가 서로 독립적으로 병행하게 실행되는 것
- 동기 스레딩
	부모가 하나 이상의 자식 스레드를 생성하고 자식 스레드 모두가 종료할 때가지 기다렸다가 자신의 실행을 재개하는 방식

## 4.5 암묵적 스레딩 Implicit Threading
다중 코어 처리의 어려움을 극복하고 병행 및 병렬 응용의 설계를 도와주는 한 가지 방법은 스레딩의 생성과 관리 책임을 응용 개발자로부터 컴파일러와 실행시간 라이브러리에게 넘겨주는 암묵적 스레딩 전략을 사용한다.

- **스레드 풀**
	웹 서버의 경우, 요청을 받을 때마다 그 요청을 위해 새로운 스레드를 만들어 준다. 이 행위는 서비스할 때마다 스레드를 생서하는데 시건이 걸리고 요청마다 새 스레드를 만든다면 언젠가는 CPU시간, 메모리 공간 같은 시스템 자원이 고갈된다. 위와 같은 문제를 해결하기 위한 방법 중 하나가 **스레드 풀(pool)**이다.
	스레드 풀은 프로세스를 시작할 때 일정한 수의 스레드들을 미리 풀로 만들어두는 것이다. 서버는 요청을 받으면 스레드 풀에 제출하고 풀에 사용 가능한 스레드들이 깨어나고 사용 가능한 스레드가 없으면 대기한다.
	스레드 풀의 장점은
	1. 새 스레드를 만들어 주기보다 기존 스레드로 서비스해 주는 것이 종종 더 빠르다.
	2. 스레드 풀은 임의 시각에 존재할 수레드 개수에 제한을 둔다. 이러한 제한은 많은 수의 스레드를 병렬 처리할 수 없는 시스템에 도움이 된다.
	3. 태스크를 생성하는 방법을 태스크로부터 분리하면 태스크를 실행을 다르게 할 수 있다.
<br>

- **Fork Join**
	메인 부모 스레드가 하나 이상의 자식 스레드를 생성(fork)한 다음 자식의 종료를 기다린 후 join하고 그 시점부터 자식의 결과를 확인하고 결합할 수 있다.
	암시적 스레딩 상황에서, fork 단계에서는 스레드가 직접 구축되지 않고 대신 병렬 작업이 식별된다. 라이브러리는 생성되는 스레드 수를 관리하며 스레드에 작업 배정을 책임진다.
<br>

- **OpenMP**
	OpenMP는 C, C++ 또는 FORTRAN으로 작성된 API와 컴파일러 디렉티브의 집합이다. OpenMP는 공유 메모리 환경에서 병렬 프로그래밍을 할 수 있도록 도움을 준다.
	OpenMP는 병렬로 실행될 수 있는 블록을 찾아 병렬 영역(parallel regions)이라고 부른다.
<br>

- **Grand Central Dispatch**
<br>

- **Intel 스레드 빌링 블록**
<br>

## **4.6 스레드와 관련된 문제들 Threading Issues**

- **Fork() 및 Exec() 시스템 콜**
	만일 한 프로그램의 스레드가 fork()와 exec()를 호출하면 새로운 프로세스는 모든 스레드를 복제해야 하는가 아니면 한 개의 스레드만 가지는 프로세스야 하는가? 몇몇 UNIX기종은 두 가지 버전 fork()를 제공한다.
	어떤 스레드가 exec() 시스템 콜을 부르면 exec()의 매개변수로 지정된 프로그램이 모든 스레드를 포함한 전체 프로세스를 대체시킨다.
<br>

- **신호 처리 Signal Handling**
	신호는 UNIX에서 프로세스에 어떤 이벤트가 일어났음을 알려주기 위해 사용된다. 신호는 알려줄 이벤트의 근원지나 이유에 따라 동기식 또는 비동기식으로 전달될 수 있다.
	모든 신호는 다믕과 같은 형태로 전달된다.
	1. 신호는 특정 이벤트가 일어나야 생성된다.
	2. 생성된 신호가 프로세스에 전달된다.
	3. 신호가 전달되면 반드시 처리되어야 한다.

	동기식 신호의 예로는 불법적인 메모리 접근, 0으로 나누기 등이 있다. 비동식 신호는 control + C 같은 특수한 키를 눌러서 프로세스를 강제 종료시키거나 타이머가 만료되는 경우 등등이다.
	모든 신호는 둘 중 하나의 처리기에 의해 처리된다.
	1. 디폴트 신호 처리기
	2. 사용자 정의 신호 처리기

	다중 스레드 프로그램에서의 신호 처리는 더욱 복잡하다. 일반적으로 다음과 같은 선택이 존재한다.
	1. 신호가 적용될 스레드에게 전달한다.
	2. 모든 스레드에 전달한다.
	3. 몇몇 스레드들에만 선택적으로 전달한다.
	4. 특정 스레드가 모든 신호를 전달받도록 지정한다.
<br>

- **스레드 취소 Thread Cancellatioin**
	스레드 취소는 스레드가 끝나기 전에 그것을 강제 종료시키는 작업을 일컫는다. 취소되어야 할 스레드는 목적 스레드(target thread)라고 부른다.
	목적 스레드의 취소는 두 가지 방식으로 발생할 수 있다.
	1. **비동기식 취소(asynchronous cancellation)**: 한 스레드가 즉시 목적 스레드를 강제 종료시킨다.
	2. **지연 취소(deferred cancellation)**: 목적 스레드가 주기적으로 자신이 강제 종료되어야 할지를 점검한다. 이 경우 목적 스레드가 질서정연하게 강제 종료될 수 있는 기회가 만들어진다.
<br>

- **스레드-로컬 저장장치 Thread-Local Storage**
	한 프로세스에 속한 스레드들은 그 프로세스의 데이터를 모두 공유한다. 그러나 상황에 따라서는 각 스레드가 자기만 액세스할 수 이쓴ㄴ 데이터를 가져야 할 필요도 있다. 그러한 데이터를 스레드-로컬 저장장치라고 부른다.
<br>

- **스케줄러 액티베이션 Scheduler Activations**
	스레드 라이브러리와 커널의 통신 문제도 고려해야한다. 다대다 또는 두 수준 모델을 구현하는 많은 시스템은 사용자와 커널 스레드 사이에 중간 자료구조를 둔다. 이를 통상 **경량 프로세스** 또는 **LWP**라고 불린다.
	커널은 응용에 가상 처리기(LWP)의 집합을 제공하고 응용은 사용자 스레드로 스케줄 하는 방법을 스케줄러 액티베이션이라고 한다. 커널은 응용에게 특정 이벤트에 대해 알려줘야 한다. 이 프로시저를 **upcall**이라고 한다.
<br>

## 4.7 운영체제 사례 Operating-System Examples
