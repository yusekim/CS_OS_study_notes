##운영체제를 살펴보기 위한 세 가지 유리한 관점##
1. 운영체제가 제공하는 서비스에 초점을 맞추는 것.
2. 운영체제가 사용자와 프로그래머에게 저공하는 인터페이스에 초점을 맞추는 것.
3. 시스템의 구성요소와 그들의 상호 연결에 초점을 맞추는 것.

---
## 2.1 운영체제 서비스

<그림 2.1>
- __사용자 인터페이스(user interface)__
	1. 그래픽 사용자 인터페이스 (GUI) : 윈도 시스템으로 I/O 지시, 메뉴에서 선택, 화면을 선택하는 포인시 장치인 마우스와 키보드를 가지고 있다.
	2. 명령어 라인 인터페이스 (CUI) : 명령을 사용하며 이를 입력할 방법(특정 옵션이 정해진 특정 형식으로 명령을 입력하기 위한 키보드)가 사용된다.
	3. 터치 스크린 인터페이스 : 휴대용 기기(모바일 시스템)
<br>
- __프로그램 수행(Program execution)__
	시스템은 프로그램을 메모리에 적재해 실행 할 수 있어야 한다. 프로그램은 정상적이든 ,혹은 비정상적이든(오류를 표시하면서) 실행을 끝낼 수 있어야 한다.
<br>
- __입출력 연산(I/O operation)__
	수행 중인 프로그램은 입출력을 요구할 수 있다. 효율과 보호를 위해, 사용자들은 통상 입출력 장치를 직접 제어할 수 없다 -> 운영체제가 입출력 수행의 수단을 제공해야 한다.
<br>
- __파일 시스템 조작(File system manipulation)__
	특히 중요한 분야. 프로그램은 파일을 읽고 쓸 필요가 있고, 이름에 의해 생성 및 삭제, 탐색과 정보열거가 가능해야 한다.
	몇몇 프로그램은 파일 소유권에 기반을 둔 권한관리를 이용해 파일이나 디렉터리의 접근을 허가하거나 거부할 수 있게 한다.
<br>
- __통신(communication)__
	1. 동일한 컴퓨터에서 수행되고 있는 프로세스들 사이에서 일어나는 통신
	2. 네트워크에 의해 함께 묶여 있는 서로 다른 컴퓨터 시스템상에서 수행되는 프로세스들 사이에서 일어나는 통신
	통신은 공유 메모리와 메시지 전달 기법을 사용하여 구현될 수 있다.
	메시지 전달 기법(message passing)의 경우 정보의 패킷들이 운영체제에 의해 프로세스들 사이를 이동한다.
<br>
- __오류 탐지(Error detection)__
	운영체제는 모든 가능한 오류를 항상 의식하고 있어야 한다.
	운영체제는 올바르고 일관성 있는 계산을 보장하기 위해 각 유형의 오류에 대해 적당한 조처를 해야 한다.
<br>
- __자원 할당(Resource allocation)__
	다수의 프로세스나 다수의 작업이 동시에 실행될 때, 그들 각각에 자원을 할당하고, 관리해 주어야 한다.
<br>
- __기록 작성(Logging)__
	우리는 어떤 프로그램이 어떤 종류의 컴퓨터 자원을 얼마나 많이 사용하는지를 추적할 수 있길 원한다.
	이러한 기록 관리는 회계(사용자에게 청구서를 보낼 수 있도록), 또는 단순히 사용 통계를 내기 위해 사용된다.
<br>
- __보호(Protection)와 보안(Security)__
	다중 사용자 컴퓨터 시스템 또는 네트워크로 연결된 컴퓨터 시스템에 저장된 정보의 소유자는 그 정보의 사용을 통제하길 원한다.
	여러 프로세스가 병행하게 수행될 때, 한 프로세스가 다른 프로세스나 운영체제 자체를 방해해서는 안 된다.
	보호는 시스템 자원에 대한 모든 접근이 통제되도록 보장하는 것을 필요로 한다.
	보안은 각 사용자가 자원에 대한 접근을 원할 때 통상 패스워드를 사용해서 시스템에게 자기 자신을 인증하는 것으로부터 시작된다.
	보안은 네트워크 어댑터 등과 같은 외부 입출력 장치들을 부적합한 접근 시도로부터 지키고, 침입의 탐지를 위해 모든 접속을 기록한다.
---

## 2.2 사용자와 운영체제 인터페이스

- __명령 인터프리터(Command-Interpreter)__
	Linux, UNIX 및 Windows를 포함한 운영체제 대부분은 명령 인터프리터를 프로세스가 시작되거나 사용자가(대화형 시스템상에서) 처음 로그온 할 때 수행되는 특수한 프로그램으로 취급한다.
	이 해석기는 셸(Shell)이라고 불리며, 사용자가 지정한 명령을 가져와서 그것을 수행한다. 이 수준에서 제공된 많은 명령은 파일을 조작한다. 즉, 생성, 삭제, 리스트, 프린트, 복사, 수행 등을 한다.
	UNIX시스템에서 사용 가능한 다양한 셸은 이런 방식으로 실행된다. 이 명령어들은 두 가지 일반적인 방식으로 구현될 수 있다.
	1. 명령 인터프리터 자체가 명령을 실행할 코드를 가지고 있는 경우이다(아마 minishell과제 수행할때 built-in 구현한거..?)
		예를 들어, 한 파일을 삭제하기 위한 명령은 명령 인터프리터가 자신의 코드의 한 부분으로 분기하고, 그 코드 부분인 매개변수를 설정하고 적절한 시스템 콜을 한다.
		이 경우 제공될 수 있는 명령의 수가 명령 인터프리터의 크기를 결정하는데, 그 이유는 각 명령이 자신의 구현 코드를 요구하기 때문..
	2. 시스템 프로그램에 의해 대부분의 명령을 구현하는 것(UNIX에 의해 사용됨)
		이러한 경우 명령 인터프리터는 전혀 그 명령을 알지 못한다. 단지 메모리에 적재되어 실행될 파일을 식별하기 위해 명령을 사용한다.
		따라서 파일을 삭제하는 UNIX 명령(rm file.txt)는 rm이라 불리는 파일을 찾아 그 파일을 메모리에 적재하고, 그것을 매개변수 file.txt로 수행한다.
		이러한 방법으로, 프로그래머는 적합한 프로그램 로직을 가진 새로운 파일을 생성함으로서 시스템에 새로운 명령을 쉽게 추가할 수 있다.
- __그래픽 기반 사용자 인터페이스(Graphical User Interface)__
	데스크톱이라고 특징지어지는 마우스를 기반으로 하는 윈도 메뉴 시스템을 사용한다.
	마우스를 움직여 마우스 포인터를 프로그램, 파일, 시스템 기능 등을 나타내는 화면상의 이미지(아이콘)에 위치시킨다.
	포인터의 위치, 마우스 버튼을 누름으로써 프로그램을 호출하거나 파일 혹은 디렉터리(폴더)를 선택할 수도 있고, 명령을 포함한 메뉴를 띄울 수 있다.
- __터치스크린 인터페이스(Touch-Screen Interface)__
	사용자는 터치스크린에서 손가락을 누르거나 스와이프 하는 등의 제스처를 취하여 상호 작용한다.
<br>
- __인터페이스의 선택(Choice of Interface)__
	컴퓨터를 관리하는 시스템 관리자와 시스템에 대해 깊게 알고 있는 파워 유저들은 명령어-라인 인터페이스가 효율적이다.
	명령어-라인 인터페이스는 보통 반복적으로 해야 하는 작업을 쉽게 할 수 있다.
	대부분의 Windows 사용자는 Windows GUI환경에서 작업하기를 원하며 셸 인터페이스는 거의 사용하지 않는다.
	iOS 및 Android 모바일 시스템은 거의 모든 사용자가 터치스크린 인터페이스를 사용하여 장치와 상호 작용한다.
___
## 2.3 시스템 콜(System Call)

시스템 콜은 운영체제에 의해 사용 가능하게 된 서비스에 대한 인터페이스를 제공한다.
특정 저수준 작업(하드웨어를 직접 접근해야 하는 작업 등)은 어셈블리 명령을 사용하여 작성되어야 하더라도 호출은 일반적으로 C, C++의 함수 형태로 제공된다.

- __예제__
	한 파일로부터 데이터를 읽어서 다른 파일로 복사하는 간단한 프로그램을 작성한다고 가정해 보자. 두 가지 방법으로 구현할 수 있다.
	`cp in.txt out.txt`
	이 명령은 입력 파일(in.txt)를 출력 파일(out.txt)에 복사한다.
	또 다른 방법은 프로그램이 사용자에게 이름을 요청하는 것이다. 대화형 시스템에서 이 방법은 일련의 시스템 콜이 필요하다.
	1. 먼저 화면에 프롬프트 메시지를 작성한 다음 키보드에서 두 파일의 이름을 지정하는 문자를 읽는다.
	2. 마우스 기바 및 아이콘 기반 시스템에서 파일 이름 메뉴는 일반적으로 창에 표시된다.
	3. 사용자는 마우스를 사용하여 소스 이름을 선택할 수 있으며 대상 이름을 지정할 수 있는 창을 열 수 있다.
_각 시스템 콜에서 오류가 발생하면 처리되어야 한다(해당 파일을 찾지 못할 경우, 파일에 대한 접근이 금지될 때 등)._
<br>
- __응용 프로그래밍 인터페이스 Application Programming Interface__
	대부분의 응용 개발자들은 응용 프로그래밍 인터페이스(application programming interface, API)에 따라 프로그램을 설계한다.
	API는 각 함수에 전달되어야 할 매개변수들과 프로그래머가 기대할 수 있는 반환 값을 포함하여 응용 프로그래머가 사용 가능한 함수의 집합을 명시한다.
	프로그래머는 운영체제가 제공하는 코드의 라이브러리를 통하여 API를 활용한다.
	왜 응용 프로그래머는 실제 시스템 콜을 부르는 것보다 API에 따라 프로그래밍 하는 걸 선호할까?
	1. 프로그램 호환성
	API에 따라 프로그램을 설계하는 응용 프로그래머는 자신의 프로그램이 같은 API를 지원하는 어느 시스템에서건 컴파일되고 실행된다는 것을 기대할 수 있다.
	실제 시스템 콜을 종종 더 자세한 명세가 필요하고 프로그램상에서 작업하기가 응용 프로그래머에게 가용한 API보다 더 어렵다.
	사실 대부분의 POSIX와 Windows API는 UNIX, Linux 및 Windows 운영체제가 제공하는 고유의 시스템 콜과 유사하다.
	2. 실행시간 환경(RTE)
	RTE는 컴파일러 또는 인터프리터를 포함하여 특정 프로그래밍 언어로 작성된 응용 프로그램을 실행하는데 필요한 전체 소프트웨어 제품군과 라이브러리 또는 로더와 같은 다른 소프트워어를 함께 가리킨다.
	RTE는 운영체제가 제공하는 스스템 콜에 대한 연결고리 역할을 하는 시스템 콜 인터페이스를 제공한다.
	시스템 콜 인터페이스는 API함수의 호출을 가로채어 필요한 운영체제 시스템 콜을 부른다.
<br>
- __시스템 콜의 유형 Types of System Calls__
	1. 프로세스 제어(Process Control)
	- 끝내기(end), 중지(abort)
	- 적재(load), 수행(execute)
	- 프로세스 생성, 프로세스 종료
	- 프로세스 속성(attributes) 획득, 프로세스 속성(attributes) 설정
	- 시간을 기다림
	- 이벤트를 기다림(wait event), 이벤트를 알림(signal event)
	- 메모리 할당 및 자유화
<br>
	2. 파일 조작
	- 파일 생성(create file), 파일 삭제(delete file)
	- 열기(open), 닫기(close)
	- 읽기, 쓰기, 위치 변경(reposition)
	- 파일 속성 획득 및 설정
<br>
	3. 장치 관리
	- 장치를 요구(request devices), 장치를 방출(relese devices)
	- 읽기, 쓰기, 위치 변경(reposition)
	- 장치 속성 획득, 장치 속성 설정
	- 장치의 논리적 부착(attach) 또는 분리(detach)
<br>
	4. 정보 유지
	- 시간과 날짜의 설정과 획득
	- 시스템 데이터의 설정과 획득
	- 프로세스, 파일, 장치 속성의 획득
	- 프로세스, 파일, 장치 속성의 설정
<br>
	5. 통신
	- 통신 연결의 생성, 제거
	- 메세지의 송신, 수신
	- 상태 정보 전달
	- 원격 장치의 부착(attach) 및 분리(detach)
<br>
	6. 보호
	- get file permissions
	- set file permissions
___
## 2.4 시스템 서비스 System Serveces

시스템 서비스(시스템 유틸리티 system utility)는 프로그램 개발과 실행을 위해 더 편리한 환경을 제공한다.
	- 파일 관리
	- 상태 정보
	- 파일 변경
	- 프로그래밍 언어 지원
	- 프로그램 적재와 실행
	- 통신
	- 백그라운드 서비스
___
## 2.5 링커와 로더 Linkers and Loaders

CPU에서 프로그램(일반적으로 이진 파일)을 실행하려면 해당 프로그램을 메모리로 가져와 프로세스 형태로 배치해야 한다. 소스 파일은 임의의 물리 메모리 위치에 적재되도록 설계된 오브젝트 파일로 컴파일 된다. 이러한 형식을 **재배치 가능 오브젝트 파일**이라고 한다. 링커는 이러한 재배치 가능 오브젝트 파일을 하나의 이진 실행 파일로 결합한다. 링킹 단계에서 표준 C또는 수학 라이브러리(플래그 -lm)와 같은 다른 오브젝트 파일 또는 라이브러리도 포함될 수 있다.
	로더는 이진 실행 파일을 메모리에 적재하는데 사용되며, CPU코어에서 실행할 수 있는 상태가 된다. 링크 및 로드와 관련된 활동은 재배치로, 프로그램 부분에 최종 주소를 할당하고 프로그램 코드와 데이터를 해당 주소와 일치하도록 조정하여 프로그램이 실행될 때 코드가 라이브러리 함수를 호출하고 변수에 접근할 수 있게 한다.
	UNIX시스템의 명령어 라인에 프로그램 이름을 입력하면(예: ./main) 셸은 먼저 fork()를 사용해 새 프로세스를 생성한 뒤, exec()콜로 로더를 호출하고 exec()에 실행 파일 이름을 전달한다. 그런 다음 로더는 새로 생성된 프로세스의 주소 공간을 사용하여 지정된 프로그램을 메모리에 적재한다. GUI 인터페이스를 사용하는 경우 실행 파일과 연관된 아이콘을 두 번 클릭하면 유사한 메커니즘을 사용하여 로더가 호출된다.
___
## 2.6 응용 프로그램이 운영체제마다 다른 이유 Why Applications Are Operating-System Specific
기본적으로 한 운영체제에서 컴파일된 응용 프로그램은 다른 운영체제에서 실행할 수 없다. 각 운영체제는 고유한 시스템 콜 집합을 제공한다. 응용 프로그램이 여러 운영체제에서 실행될 수 있게 만드는 세 가지 방법이 있다.
1. 인터프리터 언어(예: Python 또는 Ruby)로 작성된 응용 프로그램. 인터프리터는 소스 프로그램의 각 라인을 읽고, 상응하는 기계어 명령어와 운영체제의 시스템 콜을 호출한다. 기계어 코드로 구성된 응용 프로그램에 비해 성능이 떨어지고, 각 운영체제의 기능의 일부만 제공한다.
2. 실행 중인 응용 프로그램을 포함하고 있는 가상 머신을 가진 언어(Java)로 작성한다. 가상 머신은 언어의 RTE 중 일부이다. Java는 로더, 바이트코드 검증기 및 Java 응용 프로그램을 Java 가상머신으로 적재하는 기타 구성요소를 RTE로 가지고 있다. 이론적으로 모든 Java 앱은 RTE가 제공되는 어디서나 실행될 수 있다. 하지만 위의 설명한 인터프리터 시스템과 유사한 단점을 가지고 있다.
3. 컴파일러가 기기 및 운영체제 고유의 이진 파일을 생성하는 표준 언어 또는 API를 사용한 응용 프로그램. 응용 프로그램은 실행될 각 운영체제로 이식되어야 하고 이 과정은 많은 시간이 소요될 수 있다. 또한 많은 시험과 디버깅을 거쳐 프로그램의 새 버전마다 수행되어야 한다. 대표적으로 다양한 UNIX 운영체제 변종 간의 소스 코드 호환성을 유지하기 위한 POSIX API와 표준 집합을 들 수 있다.
	위의 솔루션들이 있음에도, 크로스 플랫폼 응용 프로그램을 개발하기는 여러가지 어려움이 있다.
	- 운영체제마다 헤더, 명령어 및 변수의 배치를 강제하는 응용 프로그램 이진 형식이 있다.
	- CPU는 다양한 명령어 집합을 가지며 해당 명령어가 포함된 응용 프로그램만 올바르게 실행할 수 있다.
	- 운영체제가 제공하는 시스템 콜이 운영체제마다 차이점이 있다.
___
## 2.7 운영체제 설계 및 구현 Operating-System Design and Implementation
- 설계 목표
시스템을 설계하는 데에 첫째 문제점은 시스템의 목표와 명세를 정의하는 일이다.
근본적으로 __사용자 목적__ 과 __시스템 목적__ 의 두 가지 기본 그룹으로 나눌 수 있다.
	- 기법과 정책
	__기법(mechanism)__ 으로부터 __정책(policiy)__ 을 분리하는 것은 중요한 원칙 중 하나이다.
	기법은 어떤 일을 어떻게 할 것인가를 결정하는 것이고, 정책은 무엇을 할 것인가를 결정하는 것이다.
	예를 들면, 타이머 구조는 CPU 보호를 보장하기 위한 **기법**이지만, 특정 사용자를 위해 타이머를 얼마나 오랫동안 설정할지를 결정하는 것은 **정책**적 결정이다.
	- 구현
	운영체제의 설계가 완료되면 구현되어야 한다.
	초기 운영체제는 어셈블리 언어로 작성되었다. 이제 대부분은 C또는 C++와 같은 고급 언어로 작성되며, 극히 일부의 시스템이 어셈블리 언어로 작성된다. 예를 들어, Android 시스템의 커널 대부분은 약간의 어셈블리 언어와 C로 작성되었다. Android 시스템 라이브러리의 대다수는 C/C++로 작성되며 개발자 인터페이스를 제공하는 응용 프로그램 프레임워크는 대부분 Java로 작성된다.
	고급언어나 시스템 구현 언어를 사용함으로서 코드를 빨리 작성하고, 간결하고 이해하기 쉽고, 디버그하기 쉬운 장점이 있다. 또한 컴파일러 기술의 향상은, 단순한 재 컴파일에 의해 전체 운영체제를 위해 생성된 코드를 향상시킨다. 마지막으로, 운영체제가 고급 언어로 작성된 경우 다른 하드웨어로 이식하는 것이 훨씬 쉽다.
___
## 2.8 운영체제 구조 Operating-System Structures
- 모놀리식 구조
	가장 간단한 구조, 커널의 모든 기능을 단일 주소 공간에서 실행되는 단일 정적 이진 파일에 넣는 것. 시스템 콜 인터페이스에는 오버헤드가 거의 없고 커널 안에서의 통신 속도가 빠른 이점이 있다.
- 계층적 접근
	시스템의 한 부분을 변경하면 다른 부분에 광범위한 영향을 줄 수 있으므로 모놀리식 접근법은 종종 **밀접하게 결합된** 시스템으로 불린다. 대안으로 **느슨하게 결합된** 시스템을 설계할 수 있다.
	이러한 시스템은 기능이 특정 기능 및 한정된 기능을 가진 개별적이며 작은 구성요소로 나뉘고, 이 모든 구성요소가 합쳐져 커널을 구성한다. 한 구성요소의 변경이 해당 구성요소에만 영향을 미치고 다른 구성요소에는 영향을 미치지 않으므로 시스템 구현자가 시스템의 내부 작동을 더 자유롭게 생성하고 변경할 수 있다는 장점이 있다.
	**게층적 접근 방식**은 운영체제가 여러 층으로 나뉘어져 있는 구조이다. 0층(하드웨어) 부터 N층(사용자 인터페이스)로 나뉜다. 운영체제 층은 자료구조와 상위층에서 호출할 수 있는 루틴의 집합으로 구성된다.
	계층적 접근 방식의 주된 장점은 간단한 구현과 디버깅이 있다. 층들은 자신의 하위층들의 서비스와 기능(연산)들만을 사용하도록 선택되고, 이것이 시스템의 검증과 디버깅 작업을 단순화한다.
	어떤 한 층의 디버깅이 끝나면, 그 다음 층은 이전 층의 동작이 정확하다고 가정할 수 있다. 또한 각 층은 자신부다 하위 수준의 층에 의해 제공된 연산들만 사용해 구현하기 때문에, 각 층은 특정 데이터 구조, 연산, 그리고 하드웨어의 존재를 사위층에 대해 숨기게 된다. 예시로 컴퓨터 네트워크(TCP/IP) 및 웹 응용 프로그램이 있다.
- 마이크로커널 Microkernels
	모놀리식 구조인 초기 UNIX가 확장함에 따라, 커널이 커지고 관리하기 힘들어졌다. 1980년대 중반 Carnegin-Mellon(카니지 멜론)대학교의 연구자들이 **마이크로커널** 접근 방식을 사용해 커널을 모듈화한 **Mach**란 운영체제를 개발하였다. 이 방법은 모든 중요치 않은 구성요소를 커널로부터 제거하고, 그들을 별도의 주소 공간에 존재하는 사용자 수준 프로그램으로 구현하여 운영체제를 구성하는 방법이다.
	마이크로커널의 주 기능은 클라이언트 프로그램과 역시 사용자 공간에서 수행되는 다양한 서비스 간에 통신을 제공하는 것이다. 예를 들어, 클라이언트 프로그램이 파일에 접근하기를 원하면, 파일 서버와 반드시 상호 작용해야 한다. 클라이언트 프로그램과 서비스는 결코 직접 상호 작용하지 않는다. 오히려, 그들은 마이크로커널과 메시지를 교환함으로써 간접적으로 상호 작용한다.
	마이크로커널의 장점은 운영체제의 확장이 쉽다는 것이다. 모든 새로운 서비스는 사용자 공간에 추가되며, 커널의 변경할 필요가 없다. 또 결과물 운영체제는 한 하드웨어로부터 다른 하드웨어로 이식이 쉽다. 그리고 서비스 대부분이 커널이 아닌 사용자 프로세스로 수행되기 때문에 더욱 높은 보안성과 신뢰성을 제공한다. 마이크로커널 운영체제의 가장 잘 알려진 실례는 macOS 및 iOS 운영체제의 커널 구성요소인 Darwin이다. 실제로 Darwin은 두 개의 커널로 구성되며 그중 하나는 Mach마이크로커널이다. 마이크로커널은 가중된 시스템 기능 오버헤드 때문에 성능이 나빠진다는 단점이 있다.
- 모듈 Modules
	운영체제를 설계하는 데 이용되는 최근 기술 중 최선책은 아마 **적재가능 커널 모듈(loadable kernel modules, LKM)** 일 것이다. 커널은 핵심적인 구성요소의 집합을 가지고 있고 부팅 때 또는 실행 중에 부가적인 서비스들을 모듈을 통하여 링크할 수 있다. 이러한 유형의 설계는 Linux, Max OS X, Solaris 및 Windows등의 현대 UNIX를 구현하는 일반적인 추세이다.
	중요한 부분은 커널은 핵심 서비스를 제공하고 다른 서비스들은 커널이 실행되는 동안 동적으로 구현되는 것이다. 서비스를 동적으로 링크하는 것은 새로운 기능을 직접 커널에 추가하는 것보다 바람직하다. 새로운 기능을 직접 커널에 추가하는 경우에는 수정 사항이 생길 때마다 커널을 다시 컴파일해야 한다. 예를 들어 CPU스케줄링과 메모리 관리 알고리즘은 커널에 직접 구현하고 다양한 파일 시스템을 지원하는 것은 적재가능 모듈을 통해 구현할 수 있다.
	전체적인 구조는 커널의 각 부분이 정의되고 보호된 인터페이스를 가진다는 점에서 계층 구조를 닮았다. 그러나 모듈에서 임의의 다른 모듈을 호줄할 수 있다는 점에서 계층 구조보다 유연하다. 또 중심 모듈은 핵심 기능만을 가지고 있고 다른 모듈의 적재 방법과 모듈들과 어떻게 통신하는지 안다는 점에서는 마이크로모듈을 떠올리게 되는데, 통신하기 위헤 메시지 전달을 호출할 필요가 없기 때문에 더 효율적이다.
- 하이브리드 시스템 Hybrid Systems
	다양한 구조를 결합하여 성능, 보인 및 편리성 문제를 해결하려는 혼용 구조로 구성된 운영체제가 대부분이다. 예를 들어, Linux는 운영체제 전부가 하나의 주소 공간에 존재하여 효율적인 성능을 제공하기 때문에 모놀리식 구조이지만, 모듈을 사용하기 때문에 새로운 기능을 동적으로 커널에 추가할 수 있다. Windows또한 대체적으로 모놀리식 구조라 할 수 있다. 그러나 전형적인 마이크로커널의 형태도 유지하고 있다.<br>
	**macOS와 iOS**
	macOS는 랩톱 및 컴퓨터, iOS는 모바일용으로 설계된 운영체제이다.
	1. 사용자 경험 층: 사용자가 컴퓨팅 장치와 상호 작용할 수 있는 소프트웨어 인터페이스를 정의한다.
	2. 응용 프로그램 프레임워크 층
	3. 핵심 프레임워크
	4. 커널 환경(Darwin)

	**Android**
	구글에서 개발한 Android 스마트폰과 태블릿을 위해 구글에서 개발되었으며, iOS와 달리 공개 소스이다.
	그래픽, 오디오 및 하드웨어 기능을 지원하는 다양한 프레임워크를 제공하는 계층화된 소프트웨어 스택이라는 점에서 iOS와 유사점이 있다.
---
## 2.9 운영체제 빌딩과 부팅 Building and Booting an Operating System
- 일반적으로 운영체제는 다양한 주변장치 구성을 가진 모든 종류의 컴퓨터에서 실행되도록 설계된다.
	운영체제를 처음부터 생성(빌딩)하는 경우의 절차:
	1. 운영체제 소스 코드를 작성한다
	2. 운영체제가 실행될 시스템의 운영체제를 구성한다.
	3. 운영체제를 컴파일 한다.
	4. 운영체제를 설치한다.
	5. 컴퓨터와 새 운영체제를 부팅한다.
	시스템 부팅(커널을 적재하여 컴퓨터를 시작하는 과정)의 과정
	1. **부트스트랩 프로그램** 또는 **부트 로더**라고 불리는 작은 코드가 커널의 위치를 찾는다.
	2. 커널이 메모리에 적재되고 시작된다.
	3. 커널은 하드웨어를 초기화 한다.
	4. 루트 파일 시스템이 마운트 된다.
	대부분의 운영체제의 부트 로더는 하드웨어 문제 진단, 손상된 파일 시스템 복구 및 운영체제 재설치 등의 작업을 할 수 있는 **복구 모드** 또는 **단일 사용자 모드**로 부팅할 수 있는 기능을 제공한다.
---
## 2.10 운영체제 디버깅 Operating-System Debugging
디버깅은 하드웨어와 소프트웨어에서의 시스템의 오류를 발견하고 수정하는 행위이다. 시스템에서 처리 중에 발생하는 병목 현상을 제거하여 성능을 향상시키려는 **성능 조정(Performance tuning)** 도 디버깅에 포함된다.
프로세스가 실패한다면, 오류 정보를 **로그 파일**에 기록한다. 운영체제는 또한 프로세스가 사용하던 메모리를 캡처한 **코어 덤프(core dump)** 를 취하고 차후 분석을 위해 파일로 저장한다.
커널 장애는 **크래시(crash)** 로 불리며 프로세스 장애와 마찬가지로 오류 정보가 로그 파일에 저장되고 메모리의 상태가 **크래시 덤프(crash dump)** 에 저장된다.
