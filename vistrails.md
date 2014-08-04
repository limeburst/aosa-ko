# VisTrails

VisTrails는 데이터 탐구와 시각화를 위한 오픈 소스 시스템입니다. VisTrails는 과학적 워크플로우와 시각화 시스템의 실용적인 기능들을 포함시켜 상당한 수준으로 확장합니다. VisTrails는 Kepler와 Taverna와 같은 과학적 워크플로우 시스템들처럼 기존의 응용 프로그램, 느슨하게 연결된 리소스, 그리고 라이브러리들을 정해진 규칙에 따라 접목시켜 계산적 프로세스를 만드는 것을 가능하게 만듭니다.  VisTrails는 AVS나 ParaView 같은 시각화 시스템들처럼 높은 수준의 과학적 정보시각화 기법을 제공하여 사용자들의 데이터를 다양한 시각적 표현을 통해 탐구하고 비교할 수 있게 합니다. 결과적으로, 사용자들은 자료 수집부터, 가공, 복잡한 분석, 그리고 시각화까지, 과학적 발견의 중요한 과정을 포괄하는 복잡한 작업의 흐름을 통합된 하나의 시스템에서 만들어낼 수 있습니다.

VisTrails의 특징점은 출처 기반 구조입니다\[[FSC+06](http://aosabook.org/en/bib1.html#bib:freire:vistrails)]. VisTrails는 탐구 작업의 과정과 파생된 데이터에 대한 자세한 이력을 추적하고 보존합니다. 통상적으로 워크플로우는 반복적인 작업을 자동화하기 위해 사용됐지만, 데이터 분석과 시각화 등 탐구적인 작업이 기반이 되는 응용 분야에서는 반복이 아니라 변화가 주가 됩니다. 사용자가 데이터에 대한 가설을 세우고 평가하며, 조정의 되풀이를 통해 서로 다르지만 관련된 일련의 워크플로우가 생성됩니다.

VisTrails는 이런 빠르게 바뀌는 워크플로우들을 관리할 수 있도록 설계되었습니다. VisTrails는 데이터 결과물(시각화, 그래프 등), 결과물의 기인이 되는 워크플로우, 그리고 해당 워크플로우의 실행 유래를 관리하며, 자동으로 추적된 유래의 질을 사용자들이 향상 수 있도록 정보를 추가하는 주석 기능도 제공합니다.

VisTrails는 재현 가능한 결과물을 만드는 것뿐만 아니라, 유래에 대한 정보를 이용하여 사용자들이 일련의 작업과 직관적인 인터페이스를 통해 공동으로 데이터를 분석할 수 있도록 도와줍니다. 특히, VisTrails는 임시 결과물들을 저장하여, 사용자들이 결과물에 이르게 한 행동들을 되돌아보며 논리의 과정을 반성할 수 있도록 도와줍니다. 사용자들은 워크플로우 버전들을 직관적인 방식으로 탐색하고, 결과물을 잃지 않으면서 변경 사항을 되돌리거나, 여러 워크플로우를 시각적으로 비교하고 워크플로우의 결과물들을 시각화된 스프레드시트에 나란히 두고 비교할 수 있습니다.

VisTrails는 워크플로우와 시각화 시스템의 확산을 방해한 중요한 사용성 문제를 개선하였습니다. 프로그래밍 경험이 없는 다수의 사용자를 포함한 넓은 사용자층을 지원하기 위해, 유추를 통해 워크플로우를 만들고 가다듬을 수 있고, 예제를 통해 워크플로우를 조회하고, 사용자들이 워크플로우를 대화식으로 구성할 수 있게 함과 동시에 추천 시스템을 통해 워크플로우 자동 완성을 제안하는 시스템\[[SVK+07](http://aosabook.org/en/bib1.html#bib:scheidegger:analogy)]을 통해 워크플로우 설계와 사용을 단순화시킬 수 있는 일련의 작업과 사용자 인터페이스\[[FSC+06](http://aosabook.org/en/bib1.html#bib:freire:vistrails)]를 제공합니다. 또, 우리는 (비전문가) 최종 사용자들에게 더욱 쉽게 배포할 수 있는 맞춤형 애플리케이션을 만드는 것을 도와주는 새로운 틀을 개발하기도 하였습니다.

VisTrails의 확장성은 사용자들이 도구와 라이브러리들을 접목하는 것을 간단히 할 수 있게 함은 물론, 새로운 기능들의 원형을 빠르게 구현할 수 있게 하는 기반에서 옵니다. 이러한 확장성은 VisTrails가 환경 과학, 정신 의학, 천문학, 우주론, 고에너지 물리, 양자 물리, 분자 모델링 등의 넓은 활용 영역을 가질 수 있게 하는 데에 주된 역할을 하였습니다. 

VisTrails를 오픈 소스로 유지하고 모두에게 무료로 제공하기 위해, 우리는 VisTrails를 자유, 오픈 소스 패키지만을 이용하여 개발하였습니다. VisTrails는 파이썬으로 작성되었으며, GUI 툴킷으로 (PyQt 파이썬 바인딩을 통해) Qt를 사용합니다. 넓은 응용 영역과 사용자 층을 생각하여, 우리는 이식성을 VisTrails의 기반에 두고 설계하였습니다. VisTrails는 윈도우, 맥, 리눅스에서 사용 가능합니다.

![그림 23.1: VisTrails 사용자 인터페이스의 구성 요소들](http://aosabook.org/images/vistrails/overview.png)

## 23.1. 시스템 개요

데이터 탐구의 본질은 사용자들이 관련 있는 데이터를 찾고, 찾은 데이터를 접목, 시각화하고, 또 다른 해답을 탐구함과 동시에 동료와 협업하며 결과를 알리기를 요구하는 창의적인 과정입니다. 과학적 탐구에서 흔히 볼 수 있는 데이터의 크기와 분석의 복잡성을 생각해 본다면, 창의성을 뒷받침하기 위한 도구가 필요함을 알 수 있습니다.

이러한 도구들에는 빠질 수 없는 두 가지의 기본적인 요구 사항이 있습니다. 첫 번째로, 탐구 과정을 형식적으로 기록할 수 있어야 하며, 이것은 이상적으로, 실행 가능해야 합니다. 두 번째로, 이러한 과정의 결과를 재현하고 문제를 푸는 과정을 증명할 수 있어야 하므로 체계적으로 출처를 추적할 수 있는 기능을 반드시 갖추어야 합니다. VisTrails는 이러한 요구 사항들을 고려하여 설계되었습니다.

### 23.1.1. Workflows and Workflow-Based Systems

### 23.1.1. 작업 흐름과 작업 흐름 기반 시스템

작업 흐름 시스템들은 여러 도구를 통합하는 파이프라인(작업 흐름)의 제작을 도와주며, 이를 통해 반복적인 작업과 결과 재현의 자동화를 가능하게 합니다. 작업 흐름은 다양한 작업에서 원시적인 셸 스크립트를 빠르게 대체하고 있으며, 이 추세는 상업적인 영역(Apple의 Mac OS X Automator, Yahoo! Pipes 등)은 물론 학문적인 영역(NiPype, Kepler, Taverna 등)에서도 확인할 수 있습니다.

작업 흐름은 스크립트나 고수준 언어로 작성된 프로그램들과 비해 몇 가지 이점을 가지고 있습니다. 작업 흐름은 하나의 작업 결과물을 다른 작업의 입력으로 연결함으로써 일련의 작업을 작성할 수 있는 간단한 프로그래밍 모델을 제공합니다. 그림 23.1은 기상 관측 데이터가 들어 있는 CSV 파일을 읽어 산점도를 만드는 작업 흐름을 보여줍니다.

이런 간단한 프로그래밍 모델은 작업 흐름 시스템이 프로그래밍에 대한 전문 지식이 없는 사용자들에게 적합한, 직관적인 시각적 프로그래밍 인터페이스를 제공할 수 있게 합니다. 또, 작업 흐름은 명시적인 구조를 가집니다. 매개 변수와 함께 프로세스(또는 모듈)를 나타내는 꼭짓점과 프로세스 사이의 데이터 흐름의 추적을 나타내는 변을 가지는 그래프로 볼 수 있습니다. 그림 23.1의 예시에서 `CSVReader` 모듈은 매개 변수로 파일 이름(`/weather/temp_precip.dat`)을 받아, 해당 파일을 읽어 `GetTemperature`와 `GetPrecipitation` 모듈에 전달하며, 이 모듈들은 다시 온도와 습도 값의 산점도를 생성하는 matplotlib 함수에 보냅니다.

대부분의 작업 흐름 시스템들은 특정 응용 영역을 위해 설계됩니다. 예를 들어 Taverna는 생물정보학 작업 흐름을, NiPype는 뇌영상 작업 흐름의 생성을 대상으로 합니다. VisTrails는 다른 작업 흐름 시스템들이 제공하는 대부분의 기능을 지원하지만, 여러 도구, 라이브러리, 서비스들을 접목시켜, 넓은 영역의 일반적인 탐구 작업을 대상으로 설계되었습니다.

### 23.1.2. 데이터와 작업 흐름 출처

결과물(그리고 데이터 생산물)의 출처 정보 보존의 중요성은 학계에서 잘 알려져 있습니다. (추적 기록, 계통, 계도로도 알려져 있는) 데이터 생산물의 출처는 그 생산물을 유도해 내는데 사용된 과정과 데이터를 담고 있습니다. 출처는 데이터의 보존, 데이터의 품질과 출처의 결정, 그리고 결과물의 재현과 검증을 위한 중요한 단서를 제공합니다 \[[FKSS08](http://aosabook.org/en/bib1.html#bib:freire:provenance)].

출처의 중요한 요소는, 인과 관계에 대한 정보, 즉, 입력 데이터와 매개 변수와 함께 데이터 결과물의 생성에 기인하게 되는 과정(일련의 단계)에 대한 설명입니다. 따라서 출처의 구조는 주어진 결과물을 얻기 위해 사용된 작업 흐름의 구조를 반영합니다.

실제로, 학계에서의 작업 흐름 시스템 사용을 확산시킨 촉매가 된 것은 작업 흐름 시스템이 출처를 자동으로 추적하기 위해 쉽게 사용될 수 있다는 사실이었습니다. 초기 작업 흐름 시스템들은 출처를 추적할 수 있도록 확장이 필요했지만, VisTrails는 출처 추적을 염두에 두고 설계되었습니다.

![그림 23.2: 주석으로 향상된, 탐구의 출처](http://aosabook.org/images/vistrails/overview.png)

### 23.1.3. 사용자 인터페이스와 기본 기능

그림 23.1과 그림 23.2에 VisTrail 사용자 인터페이스의 구성 요소들이 나타나 있습니다. 사용자들은 워크플로우 편집기를 통해 작업 흐름을 만들고 편집합니다.

작업 흐름 그래프를 만들기 위해 사용자들은 모듈 레지스트리에서 모듈을 끌어 워크플로우 편집 캔버스에 넣을 수 있습니다. VisTrails는 몇 가지 내장 모듈을 제공하며, 사용자들이 자신의 모듈을 추가할 수도 있습니다 (23.3에서 자세히 설명됩니다). 모듈이 선택되면, VisTrails는 사용자가 모듈의 매개 변수들을 설정하고 편집할 수 있도록 모듈의 매개 변수들을 매개 변수 편집 영역에 표시해 줍니다.

작업 흐름의 규칙이 다듬어짐과 동시에 VisTrails는 변경 사항을 추적하여 버전 트리 뷰를 통해 변경 사항들을 사용자에게 보여줍니다. 사용자들은 VisTrails 스프레드시트에서 작업 흐름과 작업 흐름의 결과물들과 상호 작용할 수 있습니다. 스프레드시트의 각 셀은 작업 흐름의 인스턴스에 대응합니다. 그림 23.1에서, 워크플로우 편집기에 나타나 있는 작업 흐름의 결과물들은 스프레드시트 왼쪽 위에 표시되어 있습니다. 사용자들은 작업 흐름의 매개 변수들을 직접 편집할 수 있으며, 스프레드시트 위의 여러 셀에 있는 매개 변수들을 동기화시킬 수도 있습니다.

버전 트리 뷰는 사용자들이 작업 흐름의 버전들을 탐색할 수 있게 도와줍니다. 그림 23.2처럼, 사용자들은 버전 트리의 노드를 클릭하여, 작업 흐름과, 연관된 결과물 (시각화 미리 보기), 그리고 메타데이터를 볼 수 있습니다. 특정 작업 흐름을 생성한 사용자의 id와 생성 날짜 등 몇몇 메타데이터는 자동으로 추적되며, 작업 흐름을 식별하기 위한 태그나 설명 등 추가적인 메타데이터를 사용자가 직접 제공할 수도 있습니다.

![Figure 23.3: VisTrails의 설계](http://aosabook.org/images/vistrails/system-interaction.png)

## 23.2. 프로젝트의 역사

VisTrails의 초기 버전은 자바와 C++로 작성되었습니다 \[[BCC+05](http://aosabook.org/en/bib1.html#bib:bavoil:vistrails)]. VisTrails의 C++ 버전은 소수의 얼리 어답터들에게 배포되었으며, 이를 통해 얻은 피드백은 VisTrails의 모습을 정하는 데에 주된 역할을 하였습니다.

여러 과학 커뮤니티 내에서 상승하는 파이썬 기반 라이브러리와 도구들의 추세를 관찰하여, VisTrails의 기반을 파이썬으로 작성하기로 하였습니다. 파이썬은 빠르게 과학 소프트웨어를 위한 보편적이며 현대적인 보조 언어로 거듭나고 있습니다. 포트란, C, C++ 등 다른 언어로 작성된 여러 라이브러리들이 스크립팅 기능을 제공하기 위해 파이썬 바인딩을 사용합니다. VisTrails는 작업 흐름에 다양한 소프트웨어 라이브러리를 접목시켜 사용할 수 있게 하는 것을 목표로 하는데, 순수 파이썬 구현체는 이것을 매우 수월하게 합니다. 특히, 파이썬에는 리습 환경에서 볼 수 있는 것들과 비슷한, 동적으로 코드를 불러오는 기능과 동시에, 훨씬 큰 개발자 커뮤니티와 풍부한 표준 라이브러리가 있습니다. 2005년 말, 우리는 파이썬/PyQt/Qt로 현재의 시스템을 개발하기 시작했습니다. 이 선택은 VisTrails의 확장, 특히 새로운 모듈과 패키지를 추가하는 것을 매우 간단히 할 수 있게 하였습니다.

VisTrail의 베타 버전은 2007년 1월에 처음 공개되었습니다. 그 이래, VisTrails는 2만 5천 번 이상 다운로드 되었습니다.

## 23.3. VisTrails의 내부

위에서 설명된 사용자 인터페이스 기능을 구현하는 내부 구성 요소들은 그림 23.3, VisTrails의 고수준 설계에 나타나 있습니다. 작업 흐름의 실행은, 실행된 명령과 명령의 매개 변수, 그리고 작업 흐름 실행의 출처(실행 출처)를 추적하는, 실행 엔진에 의해 관리됩니다. VisTrails는 중간 결과물을 메모리와 디스크에 캐싱하는 것도 실행의 일부로서 가능하게 합니다. 23.3장에서 설명되겠지만, 새로운 모듈과 매개 변수의 조합만이 재실행되며, 이들은 내재한 라이브러리(matplotlib 등)로부터의 함수를 호출함으로써 실행됩니다. 작업 흐름의 결과물들은 출처와 연결 된 후에 전자 문서에 포함될 수 있습니다 (23.4장).

작업 흐름에 대한 변경 사항 정보는 버전 트리로서 추적되며, 로컬 디렉터리의 XML 파일, 관계형 데이터베이스 등 여러 스토리지 백엔드를 사용하여 영속시킬 수 있습니다. VisTrails는 사용자들이 출처 정보를 탐색할 수 있도록 질의 엔진도 제공합니다.

VisTrails는 대화식 도구로서 설계되었지만, 서버 모드로도 사용할 수 있습니다. 작업 흐름은 생성된 이후 VisTrails 서버에 의해 실행될 수 있습니다. 이 기능은, 웹 기반 인터페이스를 만들어 이를 통해 사용자들이 작업 흐름과 상호 작용하거나, 고성능 컴퓨팅 환경에서 작업 흐름을 실행하는 등 몇몇 상황에서 유용하게 사용될 수 있습니다.

### 23.3.1. 버전 트리: 변경점 기반 출처

![그림 23.4: 변경점 기반 출처 모델](http://aosabook.org/images/vistrails/change-based-prov.png)

우리는 VisTrails에서 작업 흐름 변화의 출처\[[FSC+06](http://aosabook.org/en/bib1.html#bib:freire:vistrails)]의 개념을 새롭게 도입하였습니다. 파생된 데이터에 대한 출처만 보존하는 이전 작업 흐름과 작업 흐름 기반의 시각화 시스템과 대비하여, VisTrails는 작업 흐름 역시 1순위 데이터 항목으로 취급하며, 이에 대한 출처 역시 추적합니다. 작업 흐름 변화에 대한 출처 정보는 반성적 사고를 할 수 있게 합니다. 사용자들은 결과물을 잃지 않으면서 여러 논리 구조를 탐색할 수 있으며, VisTrails가 중간 결과물을 저장하기 때문에, 이러한 정보를 이용해서 증명, 추론할 수 있습니다. 이는 탐구 과정을 단순화시킬 수 있는 작업들을 가능하게 하기도 합니다. 예를 들어, 사용자들은 주어진 작업에 대해 생성된 작업 흐름 공간의 탐색, 작업 흐름과 그 결과를 시각적으로 비교(그림 23.4), 매개 변수 영역을 탐색하는 등의 작업들을 쉽게 할 수 있습니다. 또, 출처 정보를 조회하여 예시를 통해 학습할 수도 있습니다.

작업 흐름의 변화는 변경점 기반의 출처 모델을 사용하여 추적됩니다. 그림 23.4에 나타난 것 처럼, VisTrails는 작업 흐름에 적용된 작업들이나 변경점(모듈의 추가, 매개 변수의 수정 등)들을 데이터베이스 트랜잭션 기록과 유사하게 저장합니다. 이 정보는 각 작업 흐름의 버전에 대응되는 노드, 자식을 얻기 위해 부모에 반영된 변경점이 변에 대응되는 트리 구조로 모델링됩니다. 우리는 이 트리를 버전 트리 또는 vistrail(visual trail의 줄임말)이라고 부릅니다. 변경점 기반의 모델이 매개 변수들의 값과 작업 흐름의 정의를 균일하게 추적한다는 점을 보면, 이 일련의 변경점들이 데이터 결과물의 출처를 결정짓기에 충분하고, 작업 흐름이 시간이 지나며 어떻게 변해왔는지에 대한 정보 역시 추적한다는 것을 알 수 있습니다. 이 모델은 간단하면서도 효율적입니다; 여러 버전의 작업 흐름을 저장하는 것에 비해 상당히 적은 공간을 사용합니다.

이 모델을 사용함으로써 얻는 몇 가지 이점들이 있습니다. 그림 23.4는 VisTrail이 두 작업 흐름을 비교하기 위해 제공하는 시각적 변경점 기능을 보여줍니다. 작업 흐름이 그래프로 표현되어 있지만, 변경점 기반 모델을 사용하기 때문에 두 작업 흐름의 비교가 매우 쉬워집니다. 버전 트리를 탐색하며 하나의 작업 흐름이 다른 작업 흐름으로 변환되는 데 필요한 일련의 작업들을 확인하는 것으로 충분합니다.

변경점 기반 모델의 또 다른 중요한 이점은, 모델의 기반이 되는 버전 트리가 협업을 위한 체계로써 사용될 수 있다는 것입니다. 작업 흐름을 설계하는 일은 어려운 작업으로 악명이 높아 여러 사용자의 협업이 필요합니다. 버전 트리가 서로 다른 사용자들의 기여를 시각화하기에 직관적인 방식을 제공할 뿐만이 아니라(해당 작업 흐름을 작성한 사용자에 따라 노드에 색을 칠하는 등), 모델의 단조로움이 단순한 알고리즘만으로도 변경점을 여러 사용자 간 동기화 할 수 있게 해줍니다. 

출처 정보는 작업 흐름이 실행되는 중에 쉽게 추적될 수 있습니다. 실행이 완료된 후에, 데이터 결과물과 그 출처, 즉, 데이터 결과물을 기인한 작업 흐름, 매개 변수, 그리고 입력 파일들과의 강한 관계를 유지하는 것 역시 중요합니다. 데이터 파일이나 출처가 옮겨졌거나 편집되었을 경우, 그 출처와 연관된 데이터나, 데이터와 연관된 출처를 찾기가 어려워질 수도 있습니다. VisTrails는 입력, 중간 데이터, 그리고 출력 데이터 파일을 영속적으로 저장하는 체계를 제공하여 출처와 데이터의 관계를 강하게 유지할 수 있게 합니다. 이 체계는 출처 정보에 언급된 데이터를 쉽고 정확하게 찾을 수 있게 하므로 재현성을 강화합니다. 이러한 관리 방식은, 중간 데이터를 캐싱하여 다른 사용자들과 공유할 수 있게 해준다는 점에서도 중요한 이점을 가집니다. 

### 23.3.2. 작업 흐름의 실행과 캐싱

VisTrails의 실행 엔진은 기존 및 새로운 도구와 라이브러리들과 접목될 수 있게 설계되었습니다. 우리는 써드 파티 과학적 시각화 및 계산 소프트웨어를 감싸는 다른 보편적인 방식들을 수용하려고 노력하였습니다. VisTrails는 특히, 입력과 출력을 파일로 받는 컴파일된 바이너리는 물론 내부 객체로 받는 C++/자바/파이썬 클래스 형태의 어플리케이션 라이브러리와도 접목될 수 있습니다.

VisTrails는 각 모듈이 계산을 하여 생성된 데이터가 모듈 간 존재하는 연결을 통해 흐르는 모듈 데이터 흐름 실행 모델을 도입하였습니다. 모듈들은 상향식으로 실행됩니다. 각 입력은 필요할 때 마다 업스트림 모듈을 재귀적으로 실행하여(모듈 A에서 B로 가는 일련의 연결이 있을 때 모듈 A가 모듈 B의 업스트림이라고 부릅니다) 생성됩니다. 중간 데이터는 (파이썬 객체의 형태로) 메모리 또는 (데이터에 접근하기 위한 정보를 포함한 파이썬 객체로 감싼 형태로) 디스크에 임시로 저장됩니다.

사용자들이 VisTrails에 직접 기능을 추가할 수 있도록 우리는 확장 가능한 패키지 시스템(23.3장에서 자세히 설명됩니다)을 만들었습니다. 패키지는 사용자들이 사용자의 모듈이나 써드 파티 모듈을 VisTrails 작업 흐름에 추가할 수 있게 합니다. 패키지 개발자는, 계산 모듈과, 계산, 그리고 각 모듈에 대한 입력과 출력 포트를 명시해야 합니다. 이미 존재하는 라이브러리에 대한 계산 메서드는, 입력 포트로부터, 이미 존재하는 함수의 매개 변수로의 번역과, 결과 값으로부터 출력 포트로의 매핑을 명시해야 합니다.

탐구 작업에 있어 공통의 하부 구조를 가지는 비슷한 작업 흐름들은 주로 잇달아 실행됩니다. 작업 흐름 실행의 효율성을 높이기 위해 VisTrails는 중간 결과를 캐싱하여 재계산을 최소화합니다. 우리는 이전 실행 결과를 재활용하기 때문에, 캐시 가능한 모듈은 함수적, 즉, 같은 입력이 주어지면, 같은 출력을 생성한다고 암시적으로 가정합니다. 이 요구 사항은 클래스에 확정적인 동작이라는 제한을 걸지만, 우리는 이것이 합리적이라고 생각합니다.

하지만, 이런 동작을 요구할 수 없는 상황들도 있습니다. 예를 들어, 파일을 원격 서버로 업로드하거나 디스크에 저장하는 모듈의 경우, 모듈의 출력은 비교적 중요하지 않지만, 이러한 모듈은 큰 부작용을 가져올 수 있습니다. 어떤 모듈들은 무작위수를 사용하며 불확정성이 바람직한 동작일 수 있습니다. 이러한 모듈들은 캐시 불가능한 것으로 표시될 수 있습니다. 하지만, 어떤 함수적이지 않은 모듈들은 함수적이도록 변환될 수 있습니다. 예를 들어, 두 파일에 데이터를 쓰는 함수는 파일들의 내용을 반환하도록 래핑될 수 있습니다.

### 23.3.3. 데이터 직렬화와 저장

출처를 지원하는 시스템의 핵심 구성 요소 중 하나는 데이터의 직렬화와 저장입니다. 기존 VisTrails는 데이터를 단순히 내부 객체(버전 트리, 모듈 등)에 정의된 `fromXML`과 `toXML` 메서드를 통해 XML로 저장하였습니다. 이런 객체들의 스키마가 변하는 것을 지원하기 위해, 이 함수들은 스키마 버전 간의 번역도 직렬화하였습니다. 프로젝트가 발전해 가며, 사용자층이 성장하였고, 우리는 관계형 저장소 등 다른 직렬화 방식도 지원할 필요가 생겼습니다. 또, 스키마 객체가 변하면서, 스키마 버전 관리, 버전 간의 번역, 개체 간 관계의 지원 같은 공통 데이터 관리 문제를 개선해야 했으며, 이를 위해 데이터베이스(db) 층을 추가하였습니다.

데이터베이스 층은 도메인 객체, 서비스 로직, 그리고 영속 메서드, 세 가지 핵심 구성 요소로 이루어져 있습니다. 도메인과 영속성 구성 요소는 각 스키마 버전이 각각의 클래스를 가질 수 있도록 버전 관리되어 있습니다. 이 방식을 통해 서로 다른 버전의 스키마를 읽기 위한 코드를 유지할 수 있습니다. 하나의 스키마 버전에서 다른 버전의 스키마로의 번역을 제공하는 메서드를 정의하는 클래스도 있습니다. 서비스 클래스는, 데이터를 다루고, 스키마 버전이 바뀌는 것을 탐지하고, 버전 간 번역을 위한 메서드를 제공합니다.

이런 코드를 작성하는 일은 장황하고 반복적이기 때문에, (메모리 첨자도 포함하는) 객체 레이아웃과 직렬화 코드를 정의하는 템플릿과 메타 스키마를 사용합니다. 메타 스키마는 XML로 작성되어 있으며, 기본 XML 직렬화나 VisTrails에 의해 정의된 관계형 매핑 외 다른 직렬화 방식을 추가하여 확장할 수 있습니다. 이 방식은 Hibernate2나 SQLObject3같은 객체 관계형 매핑이나 프레임워크와 비슷하지만, 식별자 재할당이나 객체 버전 간 번역을 위한 루틴들을 더합니다. 또, 같은 메타 스키마를 사용해 여러 언어에 대한 직렬화 코드를 생성할 수 있습니다. 초기에는 메타 스키마로부터 가져온 변수로 파이썬 코드를 실행하여 도메인과 영속성 코드를 생성했던 메타-파이썬으로 작성을 하였지만, 최근에는 Mako 템플릿으로 이전하였습니다.

자동 번역은 데이터를 새로운 버전의 VisTrails로 이전해야 하는 사용자들에게 필수적입니다. 우리 설계는 개발자들이 이러한 번역을 쉽게 구현할 수 있도록 몇 가지 훅을 제공합니다. 각 버전에 대한 코드를 보존하기 때문에, 번역 코드는 버전 간의 매핑만 하면 됩니다. 최하위 단에서. 어떠한 하나의 버전을 어떠한 다른 버전으로 변화시킬 수 있는 매핑을 정의합니다. 거리가 먼 버전 간에는 다수의 중간 버전을 거칩니다. 초기에 이 매핑은 정방향, 즉 새로운 버전이 이전 버전으로는 번역될 수 없는 매핑이었지만, 최근의 스키마 매핑에서는 역방향 매핑도 추가되었습니다.

각 객체는 서로 다른 버전의 객체를 받아 현재 버전을 반환하는 `update_version` 메서드를 가지고 있습니다. 기본값으로, 각 객체가 이전 객체의 필드를 새로운 버전의 객체로 매핑하는 방식으로 업그레이드되는 재귀적 번역을 합니다. 이 매핑은 기본값으로, 같은 이름을 가진 필드는 복사하지만, 이러한 동작을 오버라이드 할 수 있는 메서드를 정의할 수도 있습니다. 오버라이드는 이전 객체를 받아 새로운 객체를 반환하는 메서드입니다. 스키마에 대한 대부분의 변경점은 소수의 필드에만 영향을 미치기 때문에 기본 매핑이 대부분의 상황을 처리할 수 있지만, 오버라이드는 국소적인 변경 사항을 정의할 수 있는 유연한 방식을 제공합니다.

### 23.3.4. Extensibility Through Packages and Python

### 23.3.4. 파이썬과 패키지를 통한 확장성

The first prototype of VisTrails had a fixed set of modules. It was an ideal environment to develop basic ideas about the VisTrails version tree and the caching of multiple execution runs, but it severely limited long-term utility.

VisTrails의 첫 프로토타입은 고정된 집합의 모듈들을 가지고 있었습니다. 이 환경은 VisTrails 버전 트리와 다수의 실행 실시의 캐싱에 대한 기본적인 아이디어를 구현하기에는 이상적이었지만, 장기적 효용성을 심각하게 제한하였습니다.

We see VisTrails as infrastructure for computational science, and that means, literally, that the system should provide scaffolding for other tools and processes to be developed. An essential requirement of this scenario is extensibility. A typical way to achieve this involves defining a target language and writing an appropriate interpreter. This is appealing because of the intimate control it offers over execution. This appeal is amplified in light of our caching requirements. However, implementing a full-fledged programming language is a large endeavor that has never been our primary goal. More importantly, forcing users who are just trying to use VisTrails to learn an entirely new language was out of the question.

우리는 VisTrails를 계산과학을 위한 기반으로 보며, 이것은 말 그대로 VisTrails가 다른 도구와 절차가 개발되기 위한 발판을 제공해야 한다는 의미를 가집니다. 이 전개의 필수 조건은 확장성입니다. 확장성을 달성하기 위한 전형적인 방식은, 대상 언어를 정하고 적절한 인터프리터를 작성하는 일을 수반합니다. 하지만 충분한 기능을 가진 프로그래밍 언어를 구현하는 것은 매우 큰 작업이며, 우리의 주 목적은 아니었습니다. 또, 사용자들이 VisTrails를 쓰기 위해서 새로운 언어를 배워야 한다는 것은 생각할 수도 없는 일이었습니다.

We wanted a system which made it easy for a user to add custom functionality. At the same time, we needed the system to be powerful enough to express fairly complicated pieces of software. As an example, VisTrails supports the VTK visualization library5. VTK contains about 1000 classes, which change depending on compilation, configuration, and operating system. Since it seems counterproductive and ultimately hopeless to write different code paths for all these cases, we decided it was necessary to dynamically determine the set of VisTrails modules provided by any given package, and VTK naturally became our model target for a complex package.

우리는 사용자들이 VisTrails에 쉽게 기능을 추가할 수 있는 동시에, VisTrails가 복잡한 소프트웨어를 다룰 수 있을 만큼 강력하기를 원했습니다. 예를 들어, VisTrails는 VTK 시각화 라이브러리를 지원합니다. VTK는 컴파일, 설정, 운영체제에 따라 달라지는 1000여개의 클래스를 포함합니다. 이 모든 경우에 대한 코드 경로를 작성하는 일이 비생산적이고 실현 가능성이 없다고 판단하였기 때문에, 주어진 패키지가 제공하는 VisTrails 모듈의 집합을 동적으로 판단하는 게 필요하다고 생각했으며, 자연스럽게 VTK가 이러한 복잡한 패키지의 모델이 되었습니다.

Computational science was one of the areas we originally targeted, and at the time we designed the system, Python was becoming popular as "glue code" among these scientists. By specifying the behavior of user-defined VisTrails modules using Python itself, we would all but eliminate a large barrier for adoption. As it turns out, Python offers a nice infrastructure for dynamically-defined classes and reflection. Almost every definition in Python has an equivalent form as a first-class expression. The two important reflection features of Python for our package system are:

계산과학은 우리가 초기에 대상으로 한 타겟이었으며, VisTrails를 설계하는 시점에서 파이썬은 과학자들 사이에서 보조적인 언어로 인기를 끌고 있었습니다. VisTrails 모듈의 동작을 명시하는 데 파이썬을 사용하는 것은 VisTrails의 도입 장벽을 걷을 수 있다는 의미를 가졌습니다. 게다가, 파이썬은 동적으로 정의된 클래스와 그 반영을 위해 꽤 괜찮은 구조를 가졌다는 것을 알게 되었습니다. 파이썬의 거의 모든 정의가 1급 함수의 형태로 나타낼 수 있습니다. 우리의 패키지 시스템을 위한 중요한 파이썬의 반영 기능 두 가지는 다음과 같습니다:

* Python classes can be defined dynamically via function calls to the `type` callable. The return value is a representation of a class that can be used in exactly the same way that a typically-defined Python class can.
*Python modules can be imported via function calls to `__import__`, and the resulting value behaves in the same way as the identifier in a standard `import` statement. The path from which these modules come from can also be specified at runtime.

* 파이썬 클래스는 호출 가능한 `type`으로의 함수 호출을 통해 동적으로 정의할 수 있습니다. 반환값은 클래스의 표현형이며, 전형적으로 정의된 파이썬 클래스와 같은 방식으로 사용할 수 있습니다.
* 파이썬 모듈은 `__import__`으로의 함수 호출로 들여올 수 있으며, 반환값은 표준 `import` 선언문의 식별자와 같은 방식으로 작동합니다. 모듈들을 찾을 위치 또한 런타임에서 정의할 수 있습니다.

Using Python as our target has a few disadvantages, of course. First of all, this dynamic nature of Python means that while we would like to ensure some things like type safety of VisTrails packages, this is in general not possible. More importantly, some of the requirements for VisTrails modules, notably the ones regarding referential transparency (more on that later) cannot be enforced in Python. Still, we believe that it is worthwhile to restrict the allowed constructs in Python via cultural mechanisms, and with this caveat, Python is an extremely attractive language for software extensibility.

파이썬을 타겟으로 사용하는 것에는 몇 가지 단점도 있습니다. 먼저, 파이썬의 동적인 성질은, VisTrails 패키지의 타입 안정성을 보장하고 싶지만 그럴 수 없다는 것을 의미합니다. 더욱 중요한 것은, VisTrails 모듈에 대한 요구 사항, 특히 관계의 투명성(이후에 자세히 설명됩니다)에 대한 요구 사항은 파이썬을 사용하였을 때 강제할 수 없다는 것입니다. 그래도, 우리는 문화적 체계를 통해 파이썬에서 허용하는 구조를 제한하는 것이 할 만 하다고 생각하며, 이 체계에 대해서 유의한다면 파이썬은 소프트웨어 확장에 대해서는 아주 매력적인 언어라고 생각합니다.

### 23.3.5. VisTrails Packages and Bundles

### 23.3.5. VisTrails 패키지와 번들

A VisTrails package encapsulates a set of modules. Its most common representation in disk is the same representation as a Python package (in a possibly unfortunate naming clash). A Python package consists of a set of Python files which define Python values such as functions and classes. A VisTrails package is a Python package that respects a particular interface. It has files that define specific functions and variables. In its simplest form, a VisTrails package should be a directory containing two files: `__init__.py` and `init.py`.

VisTrails 패키지는 모듈들의 집합을 포함합니다. 디스크에 있는 VisTrails 패키지의 가장 흔한 형태는 파이썬 패키지의 형태(안타깝지만 때로는 이름이 겹치는)와 같습니다. 파이썬 패키지는 함수나 클래스 등의 값을 정의하는 파이썬 파일들의 집합으로 이루어져 있습니다. VisTrails 패키지는 특정 인터페이스를 구현하는 파이썬 패키지입니다. 특정한 함수와 변수를 정의하는 파일을 포함하고 있습니다. 가장 단순한 VisTrails 패키지는 `__init__.py` 파일과 `init.py`를 포함하는 폴더입니다. 

The first file `__init__.py` is a requirement of Python packages, and should only contain a few definitions which should be constant. Although there is no way to guarantee that this is the case, VisTrails packages failing to obey this are considered buggy. The values defined in the file include a globally unique identifier for the package which is used to distinguish modules when workflows are serialized, and package versions (package versions become important when handling workflow and package upgrades, see Section 23.4). This file can also include functions called `package_dependencies` and `package_requirements`. Since we allow VisTrails modules to subclass from other VisTrails modules beside the root `Module` class, it is conceivable for one VisTrails package to extend the behavior of another, and so one package needs to be initialized before another. These inter-package dependencies are specified by `package_dependencies`. The `package_requirements` function, on the other hand, specifies system-level library requirements which VisTrails, in some cases, can try to automatically satisfy, through its bundle abstraction.

첫번째 파일인 `__init__.py`는 파이썬 패키지의 요구 사항으로, 소수의 정적 정의만 해야 합니다. 이를 보장할 수는 없지만, 이를 따르지 않는 VisTrails 패키지는 버그가 있는 것으로 간주됩니다. 이 파일에는 패키지에 대한 고유 식별자와 패키지 버전(작업 흐름과 패키지 업그레이드를 다룰 때 버전은 중요한 정보입니다. 23.4장에 자세히 설명되어 있습니다)이 정의되어 있습니다. 이 파일은 `package_dependencies`와 `package_requirements` 함수를 포함할 수도 있습니다. VisTrails 모듈은 기본 `Module` 클래스 외에도 다른 VisTrails 모듈을 상속받을 수 있으므로, VisTrails 패키지가 다른 패키지의 기능을 확장하는 것도 있을 수 있는 일이며, 따라서 해당 패키지는 다른 패키지보다 먼저 초기화되어야 합니다. 이러한 패키지간의 의존성은 `package_dependencies`에 정의됩니다. 반면, `package_requirements` 함수는 시스템 레벨 라이브러리 종속성을 정의하며, VisTrails는 이러한 종속성들을 번들 추상화를 통해 종종 자동으로 충족시킬 수 있습니다.

A bundle is a system-level package that VisTrails manages via system-specific tools such as RedHat's RPM or Ubuntu's APT. When these properties are satisfied, VisTrails can determine the package properties by directly importing the Python module and accessing the appropriate variables.

번들은 VisTrails가 RedHat의 RPM이나 Ubuntu의 APT처럼 시스템 종속적인 도구를 통해 관리하는 시스템 레벨 패키지입니다. 이러한 속성을 만족시킬 때, VisTrails는 파이썬 모듈을 직접 임포트하여 필요한 변수들을 접근함으로서 패키지의 속성을 판단할 수 있습니다.

The second file, `init.py`, contains the entry points for all the actual VisTrails module definitions. The most important feature of this file is the definition of two functions, `initialize` and `finalize`. The `initialize` function is called when a package is enabled, after all the dependent packages have themselves been enabled. It performs setup tasks for all of the modules in a package. The `finalize` function, on the other hand, is usually used to release runtime resources (for example, temporary files created by the package can be cleaned up).

두번째 파일인 `init.py`는 실제 VisTrails 모듈 정의의 진입점을 포함합니다. 이 파일의 가장 중요한 특징은, `initialize`와 `finalize` 두 함수의 정의입니다. `initialize` 함수는 패키지가 활성화 될 때 의존 패키지들이 모두 활성화 된 후 호출되며, 패키지 안의 모든 모듈들에 대한 구성 작업을 실행합니다. `finalize` 함수는 런타임 자원(패키지가 생성한 임시 파일 등)을 할당 해재할 때 사용됩니다.

Each VisTrails module is represented in a package by one Python class. To register this class in VisTrails, a package developer calls the `add_module` function once for each VisTrails module. These VisTrails modules can be arbitrary Python classes, but they must respect a few requirements. The first of these is that each must be a subclass of a basic Python class defined by VisTrails called, perhaps boringly, `Module`. VisTrails modules can use multiple inheritance, but only one of the classes should be a VisTrails module—no diamond hierarchies in the VisTrails module tree are allowed. Multiple inheritance becomes useful in particular to define class mix-ins: simple behaviors encoded by parent classes which can be composed together to create more complicated behaviors.

각 VisTrails 모듈은 패키지 안의 하나의 파이썬 클래스에 의해 대표됩니다. 이 클래스를 VisTrails에 등록하기 위해서 패키지 개발자는 VisTrails 모듈 마다 `add_module` 함수를 호출합니다. 이 VisTrails 모듈들은 임의의 파이썬 클래스이지만, 몇 가지 요구 사항을 충족해야 합니다. 첫번째 요구사항은, VisTrails가 정의하는, 재미 없을지도 모르겠지만, `Module`이라고 불리는 기초 파이썬 클래스를 상속해야 한다는 것입니다. VisTrails 모듈은 다중 상속을 사용할 수 있지만, 하나의 클래스만이 VisTrails 모듈이어야 합니다. VisTrails 모듈 트리에서는 다이아몬드 계층을 허용하지 않습니다. 다중 상속은 클래스 믹스인을 정의할 때 유용합니다. 단순한 동작을 가지는 부모 클래스들을 함께 구성하여 복잡한 작업을 할 수 있습니다.

The set of available ports determine the interface of a VisTrails module, and so impact not only the display of these modules but also their connectivity to other modules. These ports, then, must be explicitly described to the VisTrails infrastructure. This can be done either by making appropriate calls to `add_input_port` and `add_output_port` during the call to `initialize`, or by specifying the per-class lists `_input_ports` and `_output_ports` for each VisTrails module.

사용 가능한 포트의 집합은 VisTrails 모듈의 인터페이스를 정의하며, 모듈의 표시 뿐만이 아니라 다른 모듈로의 연결성에도 영향을 미치게 됩니다. 이 포트들은 VisTrails에 명시적으로 알려져야 합니다. 이 작업은 `initialize`를 호출하는 중에 `add_input_port`와 `add_output_port`을 호출하거나, 각 VisTrails 모듈 마다 클래스에 `_input_ports`와 `_output_ports` 리스트를 정의함으로서 할 수 있습니다.

Each module specifies the computation to be performed by overriding the `compute` method. Data is passed between modules through ports, and accessed through the `get_input_from_port` and `set_result` methods. In traditional dataflow environments, execution order is specified on-demand by the data requests. In our case, the execution order is specified by the topological sorting of the workflow modules. Since the caching algorithm requires an acyclic graph, we schedule the execution in reverse topological sorted order, so the calls to these functions do not trigger executions of upstream modules. We made this decision deliberately: it makes it simpler to consider the behavior of each module separately from all the others, which makes our caching strategy simpler and more robust.

각 모듈은 `compute` 메서드를 오버라이딩하여 수행할 계산을 정의합니다. 데이터는 포트를 통해 모듈 간 전달되며, `get_input_from_port`와 `set_result` 메서드를 통해 접근됩니다. 전통적인 데이터 흐름 환경에서 실행 순서는 데이터 요청에 의해 필요에 따라 결정되지만, VisTrails의 경우 작업 흐름 모듈의 위상순서에 따라 결정됩니다. 캐싱 알고리즘이 비순환적 그래프를 요구하므로, 우리는 함수 호출이 업스트림 모듈의 실행을 야기하지 않도록 실행 순서를 역위상순으로 정렬하여 스케쥴링합니다. 우리는 이 결정을 고의로 내렸으며, 각 모듈의 동작을 단독으로 고려하기 간편해지고, 캐싱 전략을 간단하고 견고하게 만들 수 있었습니다.

As a general guideline, VisTrails modules should refrain from using functions with side-effects during the evaluation of the `compute` method. As discussed in Section 23.3, this requirement makes caching of partial workflow runs possible: if a module respects this property, then its behavior is a function of the outputs of upstream modules. Every acyclic subgraph then only needs to be computed once, and the results can be reused.

일반적인 지침으로, VisTrails 모듈은 `compute` 메서드의 실행 중에 부작용을 가지는 함수의 사용을 삼가야 합니다. 23.3장에서 언급했던 것처럼, 이 요구사항은 부분적인 작업 흐름의 실행의 캐싱을 가능하게 합니다. 모듈이 이 속성을 존중한다면, 해당 모듈의 동작은 업스트림 모듈의 결과물에 함수적입니다. 따라서 모든 비순환식 부분 그래프는 한 번만 계산되면 되고, 결과물을 재사용할 수 있게 됩니다.

### 23.3.6. Passing Data as Modules

### 23.3.6. 데이터를 모듈로서 전달하기

One peculiar feature of VisTrails modules and their communication is that the data that is passed between VisTrails modules are themselves VisTrails modules. In VisTrails, there is a single hierarchy for module and data classes. For example, a module can provide itself as an output of a computation (and, in fact, every module provides a default "self" output port). The main disadvantage is the loss of conceptual separation between computation and data that is sometimes seen in dataflow-based architectures. There are, however, two big advantages. The first is that this closely mimics the object type systems of Java and C++, and the choice was not accidental: it was very important for us to support automatic wrapping of large class libraries such as VTK. These libraries allow objects to produce other objects as computational results, making a wrapping that distinguishes between computation and data more complicated.

VisTrails 모듈과 모듈간 통신의 특이한 점은, 모듈 간 전달되는 데이터 자체도 VisTrails 모듈이라는 점입니다. VisTrails에는 모듈과 데이터 클래스 위한 하나의 계층이 있습니다. 예를 들어, 모듈은 계산의 결과로 자기 자신을 제공할 수 있습니다(사실, 모든 모듈은 기본값으로 "self" 출력 포트를 제공합니다). 이것이 주된 단점은, 데이터 흐름 기반 설계에서 가끔 보이는, 계산과 데이터의 개념적인 분리의 상실을 야기한다는 점입니다. 하지만 두 가지 큰 장점을 얻을 수 있습니다. 첫번째는 이러한 

The second advantage this decision brings is that defining constant values and user-settable parameters in workflows becomes easier and more uniformly integrated with the rest of the system. Consider, for example, a workflow that loads a file from a location on the Web specified by a constant. This is currently specified by a GUI in which the URL can be specified as a parameter (see the Parameter Edits area in Figure 23.1). A natural modification of this workflow is to use it to fetch a URL that is computed somewhere upstream. We would like the rest of the workflow to change as little as possible. By assuming modules can output themselves, we can simply connect a string with the right value to the port corresponding to the parameter. Since the output of a constant evaluates to itself, the behavior is exactly the same as if the value had actually been specified as a constant.

이 결정의 두번째 장점은, 상수와, 사용자가 설정 가능한 매개 변수를 작업 흐름 내에서 정의하기 더 쉽고 시스템의 다른 부분과도 균일하게 통합된다는 것입니다. 상수로 정의된 웹 위치로부터 파일을 불러오는 작업 흐름을 예로 들면, URL은 매개 변수로서 GUI를 통해 지정됩니다(그림 23.1의 매개 변수 편집 영역). 이 작업 흐름을 조금 더 자연스럽게 편집을 가하자면, URL을 업스트림의 다른 곳에서 계산하여 가져 오는 것입니다. 모듈들이 자기 자신을 결과로 제공할 수 있다고 가정하여, 단지 파라미터에 해당되는 포트에 문자열을 연결하면 됩니다. 상수의 출력은 상수 자기 자신이기 때문에, 이것은 값이 상수로 지정되었을 때와 똑같이 작동합니다.

![Figure 23.5: Prototyping New Functionality with the `PythonSource` Module](http://aosabook.org/images/vistrails/python-source.png)

![그림 23.5: `PythonSource` 모듈으로 새로운 기능 프로토타이핑 하기](http://aosabook.org/images/vistrails/python-source.png)

There are other considerations involved in designing constants. Each constant type has a different ideal GUI interface for specifying values. For example, in VisTrails, a file constant module provides a file chooser dialog; a Boolean value is specified by a checkbox; a color value has a color picker native to each operating system. To achieve this generality, a developer must subclass a custom constant from the `Constant` base class and provide overrides which define an appropriate GUI widget and a string representation (so that arbitrary constants can be serialized to disk).

상수들을 설계하는 데 고려해야 할 다른 점들도 있습니다. 상수형마다 다른 값을 설정하기 위한 이상적인 GUI 인터페이스를 가집니다. 예를 들어, VisTrails에서는, 파일 상수 모듈은 파일 선택 대화 창을 제공하고, 불린 값은 체크박스로 표현되며, 색 값은 운영체제에 따른 색 선택 창을 가집니다. 이러한 일반성을 가지기 위해, 개발자는 `Constant` 기반 클래스를 상속하고, 적절한 GUI 위젯을 정의하는 오버라이드를 제공하고, 문자열 표현형을 정의해야 합니다(임의의 상수들이 디스크에 직렬화될 수 있도록). 

We note that, for simple prototyping tasks, VisTrails provides a built-in `PythonSource` module. A PythonSource module can be used to directly insert scripts into a workflow. The configuration window for PythonSource (see Figure 23.5) allows multiple input and output ports to be specified along with the Python code that is to be executed.

단순한 프로토타이핑 작업에 대해서는, VisTrails는 내장된 `PythonSource` 모듈을 제공합니다. PythonSource 모듈은 작업 흐름에 스크립트를 직접 삽입하는데 쓰일 수 있습니다. PythonSource(그림 23.5)의 설정 창은 다수의 입력과 출력 포트와 함께 실행될 파이썬 코드의 입력을 지원합니다.

## 23.4. 구성 요소와 기능

위에서 설명된 것처럼, VisTrails는 탐구적 계산 작업의 제작과 실행을 간편하게 해 주는, 기능들과 사용자 인터페이스를 제공합니다. 아래에서 이에 관해 설명하며, VisTrails가 출처 정보가 풍부한 발행물을 만드는 기반으로서 어떻게 사용되는지에 대해서도 짧게 설명합니다. VisTrails에 대한 더욱 자세한 기능과 설명은 온라인 문서에 있습니다.

![그림 23.6: 시각화 스프레드시트](http://aosabook.org/images/vistrails/spreadsheet.png)

### 23.4.1. Visual Spreadsheet

### 23.4.1. 시각화 스프레드시트

VisTrails allows users to explore and compare results from multiple workflows using the Visual Spreadsheet (see Figure 23.6). The spreadsheet is a VisTrails package with its own interface composed of sheets and cells. Each sheet contains a set of cells and has a customizable layout. A cell contains the visual representation of a result produced by a workflow, and can be customized to display diverse types of data.

VisTrails는 시각화 스프레드시트(그림 23.6)을 통해 사용자들이 여러 작업 흐름으로부터의 결과물을 탐색하고 비교할 수 있게 합니다. 이 스프레드시트는 시트와 셀로 이루어진 인터페이스를 가진 VisTrails 패키지입니다. 각 시트는 셀의 집합을 포함하고, 커스터마이즈 가능한 레이아웃을 가집니다. 하나의 셀은 작업 흐름이 만들어낸 결과물의 시각적 표현을 포함하고, 다양한 종류의 데이터를 표현할 수 있게 변경될 수 있습니다.

To display a cell on the spreadsheet, a workflow must contain a module that is derived from the base `SpreadsheetCell` module. Each `SpreadsheetCell` module corresponds to a cell in the spreadsheet, so one workflow can generate multiple cells. The `compute` method of the `SpreadsheetCell` module handles the communication between the Execution Engine (Figure 23.3) and the spreadsheet. During execution, the spreadsheet creates a cell according to its type on-demand by taking advantage of Python's dynamic class instantiation. Thus, custom visual representations can be achieved by creating a subclass of `SpreadsheetCell` and having its `compute` method send a custom cell type to the spreadsheet. For example, the workflow in Figure 23.1, `MplFigureCell` is a `SpreadsheetCell` module designed to display images created by matplotlib.

스프레드시트에 셀을 표시하기 위해서, 작업 흐름은 `SpreadsheetCell`을 상속하는 모듈을 가지고 있어야 합니다. 각 `SpreadsheetCell` 모듈은 스프레드시트 위의 셀에 대응되며, 하나의 작업 흐름은 여러 셀을 생성할 수 있습니다. `SpreadsheetCell`의 `compute` 모듈은 실행 엔진(그림 23.3)과 스프레드시트 사이의 통신을 제어합니다. 실행 중에, 스프레드시트는 파이썬의 동적 클래스 초기화 기능을 활용하여 셀을 생성합니다. 따라서, `SpreadsheetCell`를 상속받는 클래스를 생성하여, 해당 클래스의 `compute` 메서드가 스프레드시트에 커스텀 셀 타입을 보내게 함으로서 커스텀 시각 표현을 할 수 있습니다. 예를 들어, 그림 23.1에 나와 있는 작업 흐름에서, `MplFigureCell`은 matplotlib가 생성한 이미지를 표시하도록 설계된 `SpreadsheetCell` 모듈입니다.

Since the spreadsheet uses PyQt as its GUI back end, custom cell widgets must be subclassed from PyQt's `QWidget`. They must also define the `updateContents` method, which is invoked by the spreadsheet to update the widget when new data arrives. Each cell widget may optionally define a custom toolbar by implementing the `toolbar` method; it will be displayed in the spreadsheet toolbar area when the cell is selected.

스프레드시트가 PyQt를 GUI 백엔드로 사용하기 때문에, 커스텀 셀 위젯들은 PyQt의 `QWidget`을 상속해야 합니다. 또, 새로운 데이터가 들어올 때 위젯을 갱신하기 위한 `updateContents` 메서드를 구현해야 합니다. 각 셀 위젯은 선택적으로 `toolbar` 메서드를 구현함으로서 커스텀 툴바를 정의할 수 있으며, 이 경우에 셀이 선택되었을 때 스프레드시트 툴바 영역에 정의된 툴바가 표시됩니다.

Figure 23.6 shows the spreadsheet when a VTK cell is selected, in this case, the toolbar provides specific widgets to export PDF images, save camera positions back to the workflow, and create animations. The spreadsheet package defines a customizable `QCellWidget`, which provides common features such as history replay (animation) and multi-touch events forwarding. This can be used in place of `QWidget` for faster development of new cell types.

그림 23.6은 VTK 셀이 선택되었을 때의 스프레드시트를 보여주며, 이 경우에 툴바는 PDF 이미지를 내보내거나, 카메라의 위치를 작업 흐름에 저장, 그리고 애니메이션을 생성하는 위젯들을 제공합니다. 스프레드시트 패키지는 히스토리 리플레이(애니메이션)와 멀티 터치 이벤트의 포워딩 등의 공통 기능을 제공하는 커스터마이즈 가능한 `QCellWidget`을 정의하며, 새로운 셀 타입의 빠른 개발을 위해 `QWidget` 대신 사용할 수 있습니다.

Even though the spreadsheet only accepts PyQt widgets as cell types, it is possible to integrate widgets written with other GUI toolkits. To do so, the widget must export its elements to the native platform, and PyQt can then be used to grab it. We use this approach for the `VTKCell` widget because the actual widget is written in C++. At run-time, the `VTKCell` grabs the window id, a Win32, X11, or Cocoa/Carbon handle depending on the system, and maps it to the spreadsheet canvas.

스프레드시트가 셀 타입으로 PyQt 위젯만을 허용하긴 하지만, 다른 GUI 툴킷으로 작성된 위젯을 사용할 수도 있습니다. 이를 달성하기 위해, 해당 위젯은 위젯의 구성 요소들을 PyQt를 사용하여 다시 가져올 수 있도록 네이티브 플랫폼으로 내보내야 합니다. 우리는 `VTKCell` 위젯이 실제로는 C++로 작성되어 있기 때문에 해당 위젯에 대해 이러한 접근 방식을 사용합니다. 런타임에서, `VTKCell`은 시스템에 따라 다르지만 윈도우 식별자, Win32, X11, 또는 Cocoa/Carbon 핸들을 가져와 스프레드시트 캔버스에 매핑시킵니다.

Like cells, sheets may also be customized. By default, each sheet lives in a tabbed view and has a tabular layout. However, any sheet can be undocked from the spreadsheet window, allowing multiple sheets to be visible at once. It is also possible to create a different sheet layout by subclassing the `StandardWidgetSheet`, also a PyQt widget. The `StandardWidgetSheet` manages cell layouts as well as interactions with the spreadsheet in editing mode. In editing mode, users can manipulate the cell layout and perform advanced actions on the cells, rather than interacting with cell contents. Such actions include applying analogies (see Section 23.4) and creating new workflow versions from parameter explorations.

셀 처럼, 시트 역시 커스터마이즈할 수 있습니다. 각 시트는 기본적으로 탭 뷰를 통해 접근할 수 있으며 표 형태의 레이아웃을 가집니다. 하지만, 모든 시트는 스프레드시트 창으로부터 꺼낼 수 있으며, 여러 시트를 동시에 볼 수 있게 합니다. 역시 PyQt 위젯인, `StandardWidgetSheet`를 상속함으로써 다른 시트 레이아웃을 만들 수 있습니다. `StandardWidgetSheet`는 셀 레이아웃 뿐만이 아니라 편집 모드의 스프레드시트와의 상호작용도 관리합니다. 편집 모드에서, 사용자들은 셀의 내용은 편집하지 않고, 셀 레이아웃과 셀에 대한 고급 작업을 할 수 있습니다. 이러한 작업은 비유를 적용하고(23.4장에서 자세히 설명됩니다), 매개 변수 탐색으로부터 새로운 작업 흐름을 생성하는 작업을 포함합니다. 

### 23.4.2. Visual Differences and Analogies

### 23.4.2. 시각적 차이와 비유

As we designed VisTrails, we wanted to enable the use of provenance information in addition to its capture. First, we wanted users to see the exact differences between versions, but we then realized that a more helpful feature was being able to apply these differences to other workflows. Both of these tasks are possible because VisTrails tracks the evolution of workflows.

VisTrails를 설계하면서, 출처 정보의 추적 뿐만이 아니라 사용을 할 수 있게 하고싶었습니다. 먼저, 사용자들이 버전 간의 정확한 차이점을 볼 수 있게 하고 싶었지만, 이러한 차이점을 다른 작업 흐름에 적용하는 기능이 더 유익하다는 것을 깨달았습니다. 이 두 작업은 VisTrails가 작업 흐름의 변경 이력을 추적하기 때문에 가능합니다.

Because the version tree captures all of the changes and we can invert each action, we can find a complete sequence of actions that transform one version to another. Note that some changes will cancel each other out, making it possible to compress this sequence. For example, the addition of a module that was later deleted need not be examined when computing the difference. Finally, we have some heuristics to further simplify the sequence: when the same module occurs in both workflows but was added through separate actions, we we cancel the adds and deletes.

버전 트리가 모든 변경점을 추적하고, 우리는 각 동작을 되돌릴 수 있기 때문에, 하나의 버전을 다른 버전으로 변화시키는 모든 동작들의 서열을 찾을 수 있습니다. 서로의 변경점을 상쇄하는 변경점들도 있다는 점을 보면, 이 서열을 압축시킬 수도 있습니다. 예를 들어, 나중에 삭제된 모듈의 추가는 변경점을 계산할 때 고려할 필요가 없습니다. 마지막으로, 이 서열을 조금 더 단순화시킬 수 있는 휴리스틱이 있습니다. 같은 모듈이 두 개의 작업 흐름 모두에 존재하지만 따로 추가되었을 경우, 추가와 삭제 작업을 상쇄할 수 있습니다.

From the set of changes, we can create a visual representation that shows similar and different modules, connections, and parameters. This is illustrated in Figure 23.4. Modules and connections that appear in both workflows are colored gray, and those appearing in only one are colored according to the workflow they appear in. Matching modules with different parameters are shaded a lighter gray and a user can inspect the parameter differences for a specific module in a table that shows the values in each workflow.

우리는 변경점의 서열로부터 모듈, 연결, 그리고 매개 변수의 공통점과 차이점을 그림 23.4 처럼 시각화할 수 있습니다. 두 작업 흐름 모두에 존재하는 모듈과 연결들은 회색으로, 하나의 작업 흐름에만 존재하면 해당 작업 흐름의 색으로 표시되어 있습니다. 같은 모듈이지만 다른 매개 변수를 가진 모듈들은 밝은 회색으로 표시되어 있으며, 사용자는 각 작업 흐름의 표에서 특정 모듈에 대한 매개 변수의 차이점을 살펴볼 수 있습니다.

The analogy operation allows users to take these differences and apply them to other workflows. If a user has made a set of changes to an existing workflow (e.g., changing the resolution and file format of an output image), he can apply the same changes to other workflows via an analogy. To do so, the user selects a source and a target workflow, which delimits the set of desired changes, as well as the workflow they wish to apply the analogy to. VisTrails computes the difference between the first two workflows as a template, and then determines how to remap this difference in order to apply it to the third workflow. Because it is possible to apply differences to workflows that do not exactly match the starting workflow, we need a soft matching that allows correspondences between similar modules. With this matching, we can remap the difference so the sequence of changes can be applied to the selected workflow [[SVK+07](http://aosabook.org/en/bib1.html#bib:scheidegger:analogy)]. The method is not foolproof and may generate new workflows that are not exactly what was desired. In such cases, a user may try to fix any introduced mistakes, or go back to the previous version and apply the changes manually.

유사 작업은 사용자들이 차이점들은 다른 작업 흐름에 적용할 수 있게 합니다. 사용자가 작업 흐름을 변경하였다면(e.g., 출력 이미지의 해상도와 파일 포맷을 바꿈), 유사를 통해 다른 작업 흐름에도 같은 변경점을 적용할 수 있습니다. 이것을 위해, 사용자는 원본 작업 흐름과 대상 작업 흐름을 선택하여, 적용을 원하는 변경점들을 결정하고 유사를 적용할 작업 흐름을 선택하게 됩니다. VisTrails는 첫번째와 두번째 작업 흐름을 원형으로 변경점을 계산하며, 이 변경점을 세번째 작업 흐름에 어떻게 적용할지 결정합니다. 시작점이 되는 작업 흐름과 정확히 매칭이 되지 않은 작업 흐름에 변경점을 적용할 수도 있기 때문에, 비슷한 모듈간의 소프트 매칭이 필요합니다. 이러한 매칭을 통해 선택된 작업 흐름에 일련의 변경점이 적용될 수 있도록 변경점을 재배치할 수 있습니다. 이 방법은 결코 간단하지 않으며, 원했던 것과는 다른 작업 흐름을 만들어낼 수도 있습니다. 이러한 경우엔 사용자가 직접 유사 작업의 실수들을 고치거나 이전 버전으로 되돌아가 변경점들을 수동으로 고칠 수 있습니다.

To compute the soft matching used in analogies, we want to balance local matches (identical or very similar modules) with the overall workflow structure. Note that the computation of even the identical matching is inefficient due to the hardness of subgraph isomorphism, so we need to employ a heuristic. In short, if two somewhat-similar modules in the two workflows share similar neighbors, we might conclude that these two modules function similarly and should be matched as well. More formally, we construct a product graph where each node is a possible pairing of modules in the original workflows and an edge denotes shared connections. Then, we run steps diffusing the scores at each node across the edges to neighboring nodes. This is a Markov process similar to Google's PageRank, and will eventually converge leaving a set of scores that now includes some global information. From these scores, we can determine the best matching, using a threshold to leave very dissimilar modules unpaired.

유사에 사용되는 소프트 매칭을 계산하기 위해 지역적인 유사도(같거나 매우 비슷한 모듈)를 작업 흐름의 전체적인 구조와 균형을 맞춥니다. 이를 위한 동일성 매칭을 위한 계산마저도 부분 그래프 동형이 어렵기 때문에 부족하다는 점을 보면 휴리스틱을 도입해야 함을 알 수 있습니다. 간단히 말하면, 두 개의 작업 흐름에 포함되어 있는 두 개의 약간 비슷한 모듈이 비슷한 이웃을 공유한다면, 이 두 모듈은 비슷한 동작을 하며 매칭될수도 있다고 결론지을수도 있는 것입니다. 좀 더 형식적으로 표현하자면, 우리는 각 노드가 원본 작업 흐름에 있는 페어링 가능한 모듈의 짝을 의미하며, 각 변이 노드 간 공유하는 연결을 의미하는 곱집합 그래프를 생성합니다. 그리고, 각 노드의 스코어를 변을 건너 이웃 노드에 방산하는 단계를 거칩니다. 이 작업은 Google의 PageRank와 비슷한 마르코프 과정이며, 언젠가는 전역적인 정보를 포함하는 스코어의 집합으로 수렴하게 됩니다. 우리는 이 스코어들을 통해 최선의 매칭을 결정하고 기준점을 사용해 닮지 않은 모듈들을 페어링하지 않을 수 있습니다.

### 23.4.3. Querying Provenance

### 23.4.3. 출처 조회

The provenance captured by VisTrails includes a set of workflows, each with its own structure, metadata, and execution logs. It is important that users can access and explore these data. VisTrails provides both text-based and visual (WYSIWYG) query interfaces. For information like tags, annotations, and dates, a user can use keyword search with optional markup. For example, look for all workflows with the keyword `plot` that were created by `user:~dakoop`. However, queries for specific subgraphs of a workflow are more easily represented through a visual, query-by-example interface, where users can either build the query from scratch or copy and modify an existing piece of a pipeline.

VisTrails에 의해 추적된 출처는 작업 흐름의 구조, 메타데이터, 그리고 실행 로그와 함께 작업 흐름들을 포함합니다. 이러한 출처 정보에 접근하고 탐색하는 것은 중요하기 때문에, VisTrails는 텍스트 기반 및 시각적(WYSIWYG) 출처 조회 인터페이스를 제공합니다. 태그, 주석, 날짜와 같은 정보에 대해서 사용자는 키워드 검색을, 선택적인 마크업을 사용해 사용할 수 있습니다. 예를 들어, 키워드 `plot`을 포함하는, 사용자, `user:~dakoop`의 모든 작업 흐름을 검색할 수 있습니다. 하지만, 작업 흐름의 특정 부분 그래프에 대한 조회 결과는 예시를 통한 시각 인터페이스로 더 잘 표현되며, 조회할 때엔 사용자들이 쿼리를 처음부터 작성하거나 존재하는 파이프라인을 복사하거나 편집하여 조회할 수 있습니다.

In designing this query-by-example interface, we kept most of the code from the existing Workflow Editor, with a few changes to parameter construction. For parameters, it is often useful to search for ranges or keywords rather than exact values. Thus, we added modifiers to the parameter value fields; when a user adds or edits a parameter value, they may choose to select one of these modifiers which default to exact matches. In addition to visual query construction, query results are shown visually. Matching versions are highlighted in the version tree, and any selected workflow is displayed with the matching portion highlighted. The user can exit query results mode by initiating another query or clicking a reset button.

VisTrails에서 위와 같은 예시를 통한 인터페이스를 설계하며 매개 변수 조합에 대한 몇 가지의 변경 사항을 제외하고는, 워크플로우 에디터의 코드를 사용하였습니다. 매개 변수에 대해서는, 정확한 값 보다는 구간이나 키워드로 검색하는 것이 유용합니다. 따라서, 우리는 매개 변수 값 필드에 수식문을 추가하였습니다. 사용자가 매개 변의 값을 추가하거나 편집하면, 기본적으로 정확한 값을 검색하지만, 제공되는 수식구들을 사용할 수 있습니다. 시각적 쿼리 작성과 함께, 쿼리의 결과도 시각적으로 제공됩니다. 매칭된 버전들은 버전 트리에서 강조되며, 선택된 작업 흐름들도 매칭된 부분과 함께 강조되어 보여집니다. 사용자는 새로운 쿼리를 시작하거나 초기화 버튼을 눌러 쿼리 결과 모드에서 나갈 수 있습니다.

### 23.4.4. Persistent Data

### 23.4.4. 영속 데이터

VisTrails saves the provenance of how results were derived and the specification of each step. However, reproducing a workflow run can be difficult if the data needed by the workflow is no longer available. In addition, for long-running workflows, it may be useful to store intermediate data as a persistent cache across sessions in order to avoid recomputation.

VisTrails는 결과물이 나오게 된 방식의 단계에 대한 출처와 각 단계에 대한 명세를 저장합니다. 하지만, 작업 흐름이 필요로 하는 데이터를 찾을 수 없게 되면 작업 흐름을 재현하기 힘들 수 있습니다. 또, 오랜 시간 동안 실행되는 작업 흐름의 경우엔, 재계산을 피하기 위해 중간 데이터를 세션 간 영속 캐시로서 저장하는 게 유용할 수 있습니다.

Many workflow systems store filesystem paths to data as provenance, but this approach is problematic. A user might rename a file, move the workflow to another system without copying the data, or change the data contents. In any of these cases, storing the path as provenance is not sufficient. Hashing the data and storing the hash as provenance helps to determine whether the data might have changed, but does not help one locate the data if it exists. To solve this problem, we created the Persistence Package, a VisTrails package that uses version control infrastructure to store data that can be referenced from provenance. Currently we use Git to manage the data, although other systems could easily be employed.

많은 작업 흐름 시스템들은 데이터에 대한 출처로서 파일 시스템 경로를 저장하지만, 이러한 접근 방식에는 문제가 많습니다. 사용자가 파일의 이름을 바꾸거나, 데이터를 빼놓고 작업 흐름을 다른 컴퓨터로 옮길 수도 있으며, 데이터의 내용을 바꿀 수도 있습니다. 어떤 상황에서든, 경로를 출처로서 저장하는 것은 충분하지 않습니다. 데이터의 해시를 출처로 저장하여 데이터가 바뀌었는지 확인할 수는 있지만, 데이터가 다른 곳으로 옮겨졌을 경우엔 해시는 도움이 되지 않습니다. 이 문제를 해결하기 위해, 우리는 출처로서 참고될 수 있는 데이터를 저장하기 위해 버전 관리 시스템을 기반으로 하는 VisTrails 패키지인 Persistence Package를 만들었습니다. 현재 데이터 관리를 위해 Git을 사용하고 있지만, 다른 시스템도 쉽게 도입될 수 있습니다.

We use universally unique identifiers (UUIDs) to identify data, and commit hashes from git to reference versions. If the data changes from one execution to another, a new version is checked in to the repository. Thus, the `(uuid, version)` tuple is a compound identifier to retrieve the data in any state. In addition, we store the hash of the data as well as the signature of the upstream portion of the workflow that generated it (if it is not an input). This allows one to link data that might be identified differently as well as reuse data when the same computation is run again.

우리는 데이터를 식별하기 위해 범용 고유 식별자(UUID)를 사용하고, 버전을 식별하기 위해 git 커밋 해시를 사용합니다. 데이터가 실행 간 변경되면 저장소에 새로운 버전이 등록됩니다. 따라서, `(uuid, version)` 튜플은 어떠한 상태에서는 데이터를 가져올 수 있는 컴파운드 식별자입니다. 또, 데이터의 해시 뿐만이 아니라, (입력 데이터가 아닐 경우) 데이터를 생성한 작업 흐름의 업스트림 부분의 시그니쳐도 저장합니다. 이를 통해 다르게 식별될 수 있는 데이터를 연결하거나, 동일한 계산이 다시 실행될 때 데이터를 재사용할 수 있게 합니다.

The main concern when designing this package was the way users were able to select and retrieve their data. Also, we wished to keep all data in the same repository, regardless of whether it is used as input, output, or intermediate data (an output of one workflow might be used as the input of another). There are two main modes a user might employ to identify data: choosing to create a new reference or using an existing one. Note that after the first execution, a new reference will become an existing one as it has been persisted during execution; a user may later choose to create another reference if they wish but this is a rare case. Because a user often wishes to always use the latest version of data, a reference identified without a specific version will default to the latest version.

이 패키지를 설계하면서 가장 우려되었던 점은 사용자들이 데이터를 선택하고 찾을 수 있는 방법을 설계하면서였습니다. 또, 데이터가 입력, 출력, 또는 중간 데이터인지와 관계 없이 (작업 흐름의 출력이 다른 작업 흐름의 입력으로 사용될 수도 있기 때문에) 하나의 저장소에 보관하고 싶었습니다. 사용자가 데이터를 식별하기 위해 사용하는 두 가지 주 모드가 있습니다. 새로운 참조를 만들거나 기존의 참조를 사용하는 것. 첫 실행 이후에, 새로운 참조는 실행되는 동안 존속하였기 때문에 기존 참조로 변한다는 점을 봤을 때, 사용자는 새로운 참조를 만들 수도 있지만 이것은 흔치 않은 일입니다. 사용자는 대부분의 경우 가장 최신의 데이터를 사용하고 싶어하기 때문에, 특정 버전을 가리키지 않는 참조는 기본값으로 최신 버전을 가리킵니다.

Recall that before executing a module, we recursively update all of its inputs. A persistent data module will not update its inputs if the upstream computations have already been run. To determine this, we check the signature of the upstream subworkflow against the persistent repository and retrieve the precomputed data if the signature exists. In addition, we record the data identifiers and versions as provenance so that a specific execution can be reproduced.

모듈이 실행되기 전에 모듈의 입력을 재귀적으로 갱신시킨다는 점을 상기하면, 영속 데이터 모듈은 업스트림 계산이 이미 실행되었을 경우 입력을 갱신하지 않을 것입니다. 이를 판단하기 위해, 우리는 업스트림의 부분 작업 흐름의 시그니쳐를 영속 저장소에서 조회하여, 해당 시그니쳐가 존재할 경우 미리 계산된 데이터를 가져옵니다. 추가적으로, 데이터의 식별자와 버전을 출처 정보로서 저장하여 특정 실행이 재현될 수 있게 합니다.

### 23.4.5. 업그레이드

출처는 VisTrails의 핵심이므로, 옛 작업 흐름을 새로운 버전의 패키지와 호환되도록 업그레이드할 수 있는 기능은 VisTrails의 주요 고려 사항입니다. 패키지는 제 3자에 의해서 만들어질 수 있으므로, 작업 흐름을 업그레이드하고 패키지 개발자들이 업그레이드 경로를 정의하기 위한 훅을 제공하는 기반이 필요합니다. 작업 흐름 업그레이드의 핵심은 모듈을 새로운 버전으로 바꾸는 것입니다. 이것은 옛 모듈의 연결과 매개 변수를 모두 교체하는 복잡한 작업입니다. 게다가 업그레이드 작업은 모듈에 대한 매개 변수와 연결들을 재설정, 재할당, 혹은 이름을 바꾸는 작업을 포함할 수도 있습니다(모듈 인터페이스가 바뀌는 등).

각 패키지는 (관련된 모듈들과 함께) 버전으로 태그 되어 있으며, 버전이 바뀐다면 패키지가 포함하는 모듈들도 바뀌었을 것이라고 가정합니다. 물론 일부, 혹은 대부분 모듈이 바뀌지 않았을 수도 있지만, 직접 코드 분석을 하지 않는 이상 이것은 알 수 없습니다. 하지만 인터페이스가 변경되지 않은 모듈들에 대해서는 자동 업그레이드를 시도합니다. 이를 위해 모듈을 새로운 버전으로 교체해 보고, 작동하지 않으면 예외를 던집니다. 개발자들이 모듈의 인터페이스나 이름을 바꿀 경우, 개발자들이 이러한 변경 사항들을 명시적으로 정의할 수 있도록 합니다. 이 작업을 조금 더 수월하게 할 수 있도록 개발자들이 기본 업그레이드 동작이 적용될 수 없는 부분에 대해서만 명시하면 되도록 `remap_module` 메서드를 만들었습니다. 예를 들어, 개발자가 입력 포트 `file`의 이름을 `value`로 바꾸었다면, 새 모듈이 생성되었을 때 옛 모듈의 `file`로의 연결들이 `value`로 연결될 수 있도록 매핑을 정의할 수 있습니다. 다음은 VisTrails 내장 모듈 업그레이드 경로의 예시입니다:

```
def handle_module_upgrade_request(controller, module_id, pipeline):
   module_remap = {'GetItemsFromDirectory':
                       [(None, '1.6', 'Directory',
                         {'dst_port_remap':
                              {'dir': 'value'},
                          'src_port_remap':
                              {'itemlist': 'itemList'},
                          })],
                   }
  return UpgradeWorkflowHandler.remap_module(controller, module_id, pipeline,
                                             module_remap)
```

이 코드는 옛(1.6까지의 버전들) `GetItemsFromDirect` 모듈을 사용하는 작업 흐름을 `Directory` 모듈을 대신 사용하도록 업그레이드하며, 옛 모듈의 `dir` 포트를 `value`로, `itemlist` 포트를 `itemList`로 매핑합니다.

모든 업그레이드는 업그레이드 전후의 실행들을 구별하고 비교할 수 있도록 버전 트리에 새로운 버전을 등록합니다. 업그레이드가 작업 흐름의 동작을 바꿀 수도 있기 때문에(패키지 개발자가 버그를 고치는 등), 출처 정보로서 추적되어야 합니다. 이전 버전의 VisTrails에서는 트리 안의 모든 버전을 업그레이드해야 할 수도 있습니다. 잡동사니들을 줄이기 위해 사용자가 탐색한 적이 있는 버전들만 업그레이드하며, 사용자가 작업 흐름이 편집되거나 실행될 때까지 업그레이드의 영속을 미룰 수 있게 합니다. 사용자가 해당 버전을 열람만 한다면, 업그레이드를 영속시킬 필요가 없습니다.

### 23.4.6. 출처 정보를 포함한 결과물의 공유와 발행

재현성은 과학적 방법론의 토대이지만, 계산적 실험들을 포함하는 최근의 출판물들은 결과물을 재현하거나 일반화하는 데 필요한 충분한 정보를 제공하지 못합니다. 최근 재현 가능한 결과의 출판에 대한 관심이 다시 높아지고 있습니다. 이러한 관습 확산의 가장 큰 장벽은 결과물을 재현하고 검증하는 데 필요한 모든 구성 요소(데이터, 코드, 매개 변수 설정 등)를 포함한 꾸러미를 만들기가 힘들다는 점입니다.

VisTrails는 자세한 출처의 추적과 위에 설명된 다양한 기능들을 통해 VisTrails 내에서의 계산적 실험 수행의 과정을 단순화시킵니다. 하지만 문서들을 연결하고 출처 정보를 공유하기 위해서는 그것을 위한 체계가 필요합니다.

우리는 깊은 캡션처럼 논문 안의 결과물을 출처와 연결하는 VisTrails 패키지를 개발하였습니다. 이 LaTeX 패키지를 통해, 사용자들은 VisTrails 작업 흐름에 연결되는 그림들을 삽입할 수 있습니다. 다음 LaTeX 코드는 작업 흐름의 결과를 포함하는 그림을 생성합니다:

```
\begin{figure}[t]
{
\vistrail[wfid=119,buildalways=false]{width=0.9\linewidth}
}
\caption{Visualizing a binary star system simulation. This is an image
  that was generated by embedding a workflow directly in the text.}
\label{fig:astrophysics}
\end{figure}
```

위 문서를 pdflatex를 통해 컴파일하였을 때 `\vistrails` 명령은 VisTrails 서버에 `id 119`를 가진 작업 흐름을 실행시키는 XML-RPC 요청을 보내는 파이썬 스크립트를 실행시킵니다. 이 파이썬 스크립트는 다시, 해당 작업 흐름의 결과를 받아 지정된 레이아웃 옵션(`width=0.9\linewidth`)이 적용된 링크된 LaTeX `\includegraphics` 명령들을 생성하여 PDF 문서에 포함합니다.

VisTrails의 결과물을 웹 페이지, 위키, 워드 문서, 파워포인트 프레젠테이션에 포함하는 것 역시 가능합니다. 마이크로소프트 파워포인트와 VisTrails간의 연결은 컴포넌트 객체 모델(COM)과 객체 연결 삽입(OLE) 인터페이스를 통해 이루어집니다. 객체가 파워포인트와 상호 작용하기 위해서는 최소한 `IOleObject`, `IDataObject`, 그리고 `IPersistentStorage` COM 인터페이스가 구현되어야 합니다. COM 인터페이스는 Qt의 `QAxAggregated` 추상화 클래스를 통해 구현되므로, OLE 객체를 만드는 데 필요한 `IDataObject`와 `IPersistentStorage`는 Qt에 의해 자동으로 관리됩니다. 따라서 우리는 `IOleObject` 인터페이스만 구현하면 됩니다. 이 인터페이스의 가장 중요한 메서드는 `DoVerb`입니다. 이 메서드는 객체 활성화 등 파워포인트의 특정 동작에 VisTrails가 반응할 수 있도록 합니다. 우리는 VisTrails 객체가 활성화되었을 때 VisTrails을 실행시켜 사용자들이 삽입하고 싶은 파이프라인과 상호 작용 하거나 선택할 수 있도록 구현하였습니다. 사용자가 VisTrails를 종료하면 파이프라인 결과가 파워포인트에 보이며, 파이프라인 정보는 OLE 객체와도 함께 저장됩니다.

우리는 사용자들이 출처 정보와 함께 결과물을 자유롭게 공유할 수 있도록 crowdLabs를 만들었습니다. crowdLabs는 과학자들이 데이터를 공동으로 분석하고 시각화하는 데 필요한 도구들과 확장 가능한 인프라를 제공하는 소셜 웹사이트입니다. crowdLabs는 VisTrails와 깊이 접목되어 있습니다. 사용자가 VisTrails에서 기인한 데이터를 공유하고 싶다면, VisTrails에서 바로 crowdLabs 서버에 접속하여 데이터를 올릴 수 있습니다. 데이터가 올라가면, 사용자들은 웹 브라우저를 통해 작업 흐름과 상호 작용 하거나 실행시킬 수 있습니다. 이 작업 흐름은 crowdLabs를 구동하는 VisTrails 서버에 의해 실행됩니다. 재현 가능한 발행물을 만들기 위해 VisTrails가 쓰이는 자세한 방법에 대해 알고 싶다면, http://www.vistrails.org를 보세요.

## 23.5. 얻은 교훈

운이 좋게도, 출처를 지원하는 데이터 탐색과 시각화 시스템을 만드는 것에 대해 생각하고 있었던 2004년도에는 이 일이 이렇게 도전적이거나, 지금까지 상태까지 오는 데 이렇게 오래 걸릴 줄 상상조차 하지 못했습니다. 만약 그걸 알았다면 시작조차 하지 않았을 것입니다.

초기에는, 새로운 기능들을 빠르게 프로토타이핑하고 선택된 일부 사용자들에게 보여주는 전략이 잘 작동했습니다. 초기에 받은 피드백과 격려는 프로젝트를 진행하는 데 큰 도움이 되었습니다. 사용자 피드백 없이는 VisTrails를 설계하기 불가능했을 것입니다. VisTrails의 한 측면을 강조할 수 있다면, VisTrails 대부분 기능들은 사용자 피드백의 직접적인 영향으로 설계되었다는 점입니다. 하지만 사용자들이 자주 요구하는 것이 가장 최선의 해결책이 아니라는 것을 알 필요가 있습니다. 사용자들의 요구를 잘 맞춰 주는 게 사용자들이 원하는 게 아니라는 것입니다. 우리는 VisTrails에 들어가는 기능들이 유용하고 시스템에 잘 접목될 수 있도록 몇 번이고 재설계하였습니다.

우리의 사용자 중심의 접근을 감안하면, 우리가 개발한 모든 기능들이 많이 사용될 것이라고 생각할 수도 있습니다. 안타깝게도, 그렇지는 않습니다. 종종 그 이유가 되는 것은, VisTrails의 기능들은 다른 도구에서는 찾아볼 수 없으며, 매우 특이하다는 점입니다. 예를 들어, 유사와 버전 트리조차 대부분의 사용자들에게는 생소한 개념이며, 익숙해지는 데 오래 걸립니다. 다른 중요한 문제는 문서의 부족입니다. 다른 오픈 소스 프로젝트들과 마찬가지로, 우리는 새로운 기능을 만드는 것을 이미 존재하는 기능을 문서화하는 것보다 잘 합니다. 문서화에 있어서의 뒤쳐짐은 유용한 기능들이 충분히 이용되지 않게 할 뿐만이 아니라, 메일링 리스트에 질문이 많이 올라오게 하기도 합니다.

VisTrails 같은 종류의 시스템을 사용하는 데에 있는 큰 장벽 중 하나는 VisTrails가 매우 일반화된 시스템이라는 점입니다. VisTrails의 사용성을 개선하기 위한 노력에도 불구하고, VisTrails는 일부 사용자들에게 급격한 학습 커브를 가진 복잡한 도구로 남아 있습니다. 우리는 시간이 지나고 문서가 개선되며, 시스템이 다듬어지고, 좀 더 많은 응용 분야와 분야별 예제가 생긴다면, 어떤 분야에서든 VisTrails를 도입하기 위한 기준이 완화될 것이라고 믿습니다. 또, 출처에 대한 개념이 널리 퍼지면, 사용자들이 VisTrails 개발에 들어간 철학을 좀 더 쉽게 이해할 수 있게 될 것이라고 믿습니다.

### 23.5.1. 감사의 말

VisTrails에 기여한 모든 개발자들에게 감사의 말을 전하고 싶습니다: Erik Anderson, Louis Bavoil, Clifton Brooks, Jason Callahan, Steve Callahan, Lorena Carlo, Lauro Lins, Tommy Ellkvist, Phillip Mates, Daniel Rees, 그리고 Nathan Smith. 프로젝트의 비전을 만드는 데 도움을 준 Antonio Baptista와, VisTrails를 개선, 특히 출처 정보가 풍부한 발행 기능을 연구, 개발, 그리고 릴리즈하기 위한 대부분의 자극을 준 Matthias Troyer에게 특별한 감사의 말을 전하고 싶습니다. VisTrails의 개발과 연구에는 허가 IIS 1050422, IIS-0905385, IIS 0844572, ATM-0835821, IIS-0844546, IIS-0746500, CNS-0751152, IIS-0713637, OCE-0424602, IIS-0534628, CNS-0514485, IIS-0513692, CNS-0524096, CCF-0401498, OISE-0405402, CCF-0528201, CNS-0551724, Department of Energy SciDAC (VACET과 SDM 센터들), 그리고 IBM Faculty Awards 아래 National Science Foundation의 지원이 있었습니다.
