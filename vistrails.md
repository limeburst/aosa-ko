# VisTrails

# VisTrails

VisTrails is an open-source system that supports data exploration and visualization. It includes and substantially extends useful features of scientific workflow and visualization systems. Like scientific workflow systems such as Kepler and Taverna, VisTrails allows the specification of computational processes which integrate existing applications, loosely-coupled resources, and libraries according to a set of rules. Like visualization systems such as AVS and ParaView, VisTrails makes advanced scientific and information visualization techniques available to users, allowing them to explore and compare different visual representations of their data. As a result, users can create complex workflows that encompass important steps of scientific discovery, from data gathering and manipulation to complex analyses and visualizations, all integrated in one system.

VisTrails는 데이터 조사와 시각화를 위한 오픈 소스 시스템입니다. 과학적 워크플로우와 시각화 시스템의 실용적인 기능을 포함하고 확장합니다. Kepler와 Taverna와 같은 과학적 워크플로우 시스템들처럼, VisTrails는 존재하는 응용 프로그램들과 느슨하게 연결된 리소스, 그리고 라이브러리들처럼 계산적인 절차의 열거를 정해진 규칙의 집합을 따라 가능하게 만듭니다. AVS와 ParaView와 같은 시각화 시스템들처럼, VisTrails는 사용자들에게 고등의 과학적인 정보 시각화 기법을 제공하여 사용자들의 데이터를 다양한 시각적인 표현을 탐구하고 비교할 수 있게 합니다. 결과적으로 사용자들은, 과학적 발견의 중요한 과정, 데이터 수집, 가공, 복잡한 분석과 시각화를 포함하는 복잡한 작업의 흐름을, 통합된 하나의 시스템에서 만들어낼 수 있습니다.

A distinguishing feature of VisTrails is its provenance infrastructure [FSC+06]. VisTrails captures and maintains a detailed history of the steps followed and data derived in the course of an exploratory task. Workflows have traditionally been used to automate repetitive tasks, but in applications that are exploratory in nature, such as data analysis and visualization, very little is repeated—change is the norm. As a user generates and evaluates hypotheses about their data, a series of different, but related, workflows are created as they are adjusted iteratively.

VisTrails의 차별점은 출처 기반 구조입니다. VisTrails는 탐구 작업의 과정과, 파생된 데이터의 자세한 이력을 추적하며 보존합니다. 전통적으로 워크플로우는 반복적인 작업을 자동화시키기 위해 사용되어 왔지만, 데이터 분석과 시각화 등 탐구가 주가 되는 응용 프로그램에서는 반복되는 것이 거의 없으며, 변화가 주가 됩니다. 사용자가 데이터에 대한 가설을 만들고 평가하는 과정을 거치는 것과 동시에, 조정의 되풀이를 통해 다르지만 서로 관련된 일련의 워크플로우가 생성됩니다.

VisTrails was designed to manage these rapidly-evolving workflows: it maintains provenance of data products (e.g., visualizations, plots), of the workflows that derive these products, and their executions. The system also provides annotation capabilities so users can enrich the automatically-captured provenance.

VisTrails는 이런 식으로 빠르게 바뀌는 워크플로우를 관리할 수 있도록 설계되었습니다. 데이터 결과물(e.g., 시각화, 그래프)의 유래, 이러한 결과물들의 기인이 되는 워크플로우, 그리고 그 워크플로우들의 실행의 유래를 유지, 관리합니다. 사용자들이, 자동적으로 추적된 유래에 정보를 추가하여 질을 향상시키기 위한 주석 기능도 제공합니다.

Besides enabling reproducible results, VisTrails leverages provenance information through a series of operations and intuitive user interfaces that help users to collaboratively analyze data. Notably, the system supports reflective reasoning by storing temporary results, allowing users to examine the actions that led to a result and to follow chains of reasoning backward and forward. Users can navigate workflow versions in an intuitive way, undo changes without losing results, visually compare multiple workflows and show their results side-by-side in a visualization spreadsheet.

VisTrails는 재현 가능한 결과물을 만드는 것 뿐만 아니라, 유래에 대한 정보를 사용하여 일련의 작업과 직관적인 인터페이스를 통해 사용자들이 공동으로 데이터를 분석할 수 있도록 도와줍니다. 특히, VisTrails 임시 결과물들을 저장하여, 사용자들이 결과물에 이르게 된 행동들을 되돌아보며 논리의 과정을 반성적으로 사고할 수 있게 도와줍니다. 사용자들은 워크플로우의 버전들을 직관적인 방식으로 탐색, 결과물을 잃지 않으면서 변경 사항을 되돌리거나, 여러 워크플로우들을 시각적으로 비교하고, 결과물들을 시각화된 스프레드시트에 나란히 두고 비교할 수 있습니다.

VisTrails addresses important usability issues that have hampered a wider adoption of workflow and visualization systems. To cater to a broader set of users, including many who do not have programming expertise, it provides a series of operations and user interfaces that simplify workflow design and use [FSC+06], including the ability to create and refine workflows by analogy, to query workflows by example, and to suggest workflow completions as users interactively construct their workflows using a recommendation system [SVK+07]. We have also developed a new framework that allows the creation of custom applications that can be more easily deployed to (non-expert) end users.

VisTrails는 워크플로우 및 시각화 시스템의 확산을 방해한 중요한 사용성 문제를 개선하였습니다. 프로그래밍 경험이 없는 다수의 사용자들을 포함한 넓은 사용자층을 지원하기 위해, 유추를 통해 워크플로우를 만들고 가다듬을 수 있고, 예제를 통해 워크플로우를 조회해고, 사용자들이 워크플로우를 대화식으로 구성함과 동시에 추천 시스템을 통해 워크플로우 완성을 제안하는 등의 기능을 통해 워크플로우 설계와 사용을 단순화시킬 수 있는 일련의 작업과 사용자 인터페이스를 제공합니다.

The extensibility of VisTrails comes from an infrastructure that makes it simple for users to integrate tools and libraries, as well as to quickly prototype new functions. This has been instrumental in enabling the use of the system in a wide range of application areas, including environmental sciences, psychiatry, astronomy, cosmology, high-energy physics, quantum physics, and molecular modeling.

VisTrails의 확장성은 사용자들이 도구와 라이브러리들을 접목시키는 것은 물론, 새로운 기능들의 원형을 빠르게 구현할 수 있게 하는 기반 구조에서 기인합니다. 이러한 확장성은 VisTrails가 환경 과학, 정신 의학, 천문학, 우주론, 고에너지 물리, 양자 물리, 분자 모델링 등 넓은 활용 영역을 가지는 데에 주된 역할을 하였습니다. 

To keep the system open-source and free for all, we have built VisTrails using only free, open-source packages. VisTrails is written in Python and uses Qt as its GUI toolkit (through PyQt Python bindings). Because of the broad range of users and applications, we have designed the system from the ground up with portability in mind. VisTrails runs on Windows, Mac and Linux.

VisTrails는 오픈 소스로 유지하고, 모두에게 무료로 제공하기 위해, 우리는 VisTrails를 자유, 오픈 소스 패키지만을 이용하여 만들엇습니다. VisTrails는 파이썬으로 작성되었으며, GUI 툴킷으로 Qt(PyQt 파이썬 바인딩을 통해)를 사용합니다. 넓은 응용 영역과 사용자 층을 고려하여, 우리는 VisTrails의 기반부터 이식성을 염두에 두고 설계하였습니다. VisTrails는 윈도우, 맥, 리눅스에서 사용 가능합니다.

![Figure 23.1: Components of the VisTrails User Interface](http://aosabook.org/images/vistrails/overview.png)

![그림 23.1: VisTrails 사용자 인터페이스의 구성 요소](http://aosabook.org/images/vistrails/overview.png)
