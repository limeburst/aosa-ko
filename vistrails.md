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

## 23.1. System Overview

## 23.1. 시스템 개요

Data exploration is an inherently creative process that requires users to locate relevant data, to integrate and visualize this data, to collaborate with peers while exploring different solutions, and to disseminate results. Given the size of data and complexity of analyses that are common in scientific exploration, tools are needed that better support creativity.

데이터 탐구는 본질적으로, 사용자가 연관된 데이터를 찾고, 찾은 데이터를 접목, 시각화 하고, 또 다른 답을 탐구함과 동시에 동료와 협업하며, 결과를 배포하는 것을 요구하는 창의적인 과정입니다.

There are two basic requirements for these tools that go hand in hand. First, it is important to be able to specify the exploration processes using formal descriptions, which ideally, are executable. Second, to reproduce the results of these processes as well as reason about the different steps followed to solve a problem, these tools must have the ability to systematically capture provenance. VisTrails was designed with these requirements in mind.

이러한 도구들에는 빠질 수 없는 두 가지의 기본적인 요구 사항이 있습니다. 첫 번째로, 탐구 과정을 형식적으로 기록할 수 있어야 하며, 이는 이상적으로, 실행 가능해야 합니다. 두 번째로, 이러한 과정들을 재현하거나, 문제를 푸는 과정에서 따른 단계를 증명할 수 있기 위해, 이러한 도구들은 체계적으로 출처를 추적할 수 있는 기능을 반드시 갖추어야 합니다. VisTrails는 이러한 요구 사항들을 고려하여 설계되었습니다.

### 23.1.1. Workflows and Workflow-Based Systems

### 23.1.1. 작업 흐름과 작업 흐름 기반 시스템

Workflow systems support the creation of pipelines (workflows) that combine multiple tools. As such, they enable the automation of repetitive tasks and result reproducibility. Workflows are rapidly replacing primitive shell scripts in a wide range of tasks, as evidenced by a number of workflow-based applications, both commercial (e.g., Apple's Mac OS X Automator and Yahoo! Pipes) and academic (e.g., NiPype, Kepler, and Taverna).

작업 흐름 시스템은 여러 도구를 통합시킬 수 있는 파이프라인(작업 흐름)의 제작을 지원합니다. 이를 통해 반복적인 작업과, 결과 재현의 자동화를 가능하게 합니다. 작업 흐름은 다양한 작업에서 원시적인 셸 스크립트를 빠르게 대체하고 있으며, 상업적인 영역은 물론(e.g., Apple의 Mac OS X Automator와 Yahoo! Pipes) 학문적인 영역(e.g., NiPype, Kepler, Taverna)에서도 이를 확인할 수 있습니다.

Workflows have a number of advantages compared to scripts and programs written in high-level languages. They provide a simple programming model whereby a sequence of tasks is composed by connecting the outputs of one task to the inputs of another. Figure 23.1 shows a workflow which reads a CSV file that contains weather observations and creates a scatter plot of the values.

작업 흐름은 스크립트나 고수준 언어로 작성된 프로그램들과 비교하여 몇 가지 이점을 가지고 있습니다. 작업 흐름은, 하나의 작업의 결과물을 다른 작업의 입력으로 연결함으로서 일련의 작업을 작성 할 수 있는 간단한 프로그래밍 모델을 제공합니다. 그림 23.1은 기상 관측 데이터가 들어 있는 CSV 파일을 읽어 데이터의 산점도를 만드는 작업 흐름을 보여줍니다.

This simpler programming model allows workflow systems to provide intuitive visual programming interfaces, which make them more suitable for users who do not have substantial programming expertise. Workflows also have an explicit structure: they can be viewed as graphs, where nodes represent processes (or modules) along with their parameters and edges capture the flow of data between the processes. In the example of Figure 23.1, the module CSVReader takes as a parameter a filename (/weather/temp_precip.dat), reads the file, and feeds its contents into the modules GetTemperature and GetPrecipitation, which in turn send the temperature and precipitation values to a matplotlib function that generates a scatter plot.

이러한 간단한 프로그래밍 모델은, 작업 흐름 시스템들이 프로그래밍 경험이 없는 사용자들에게 적합한 직관적인 시각적 프로그래밍 인터페이스를 제공할 수 있도록 합니다. 작업 흐름은 명시적인 구조를 가져, 노드는 프로세스(또는 모듈)를 나타내며, 매개 변수와 변이 프로세스 간의 데이터 흐름을 추적하는 구조의 그래프로 볼 수 있습니다. 그림 23.1의 예시에서, CSVReader 모듈은 매개 변수로 파일 이름(/weather/temp_precip.dat)을 받아, 파일을 읽고, 파일의 내용을 GetTemperature와 GetPrecipitation 모듈에 공급하며, 이 모듈들은 다시 온도와 습도 값을 산점도를 생성하는 matplotlib 함수에 보냅니다.

Most workflow systems are designed for a specific application area. For example, Taverna targets bioinformatics workflows, and NiPype allows the creation of neuroimaging workflows. While VisTrails supports much of the functionality provided by other workflow systems, it was designed to support general exploratory tasks in a broad range of areas, integrating multiple tools, libraries, and services.

대부분의 작업 흐름 시스템들은 특정 응용 영역을 위해 설계됩니다. 예를 들어, Taverna는 생물 정보 공학의 작업 흐름을, NiPype는 뇌영상 작업 흐름을 대상으로 합니다. VisTrails는 다른 작업 흐름 시스템들이 제공하는 대부분의 기능들을 지원하지만, 여러 도구, 라이브러리, 서비스들을 통합하여, 넓은 영역의 일반적인 탐구 작업을 주 대상으로 설계되었습니다.

### 23.1.2. Data and Workflow Provenance

### 23.1.2. 데이터와 작업 흐름 출처

The importance of keeping provenance information for results (and data products) is well recognized in the scientific community. The provenance (also referred to as the audit trail, lineage, and pedigree) of a data product contains information about the process and data used to derive the data product. Provenance provides important documentation that is key to preserving the data, to determining the data's quality and authorship, and to reproducing as well as validating the results [FKSS08].

결과물(그리고 데이터 생산물)의 출처 정보를 보존하는 것의 중요성은 학계에서 잘 알려져 있습니다. 데이터 생산물의 출처(추적 기록, 계통, 계도로도 알려져 있는)는 그 생산물을 유도해 내는데 사용된 과정과 데이터를 담고 있습니다. 출처는 데이터를 보존, 품질과 원작자를 결정, 그리고 결과의 재현과 검증을 하는 데 필수적인 정보를 제공합니다.

An important component of provenance is information about causality, i.e., a description of a process (sequence of steps) which, together with input data and parameters, caused the creation of a data product. Thus, the structure of provenance mirrors the structure of the workflow (or set of workflows) used to derive a given result set.

출처의 중요한 구성 요소는, 인과 관계에 대한 정보 즉, 입력 데이터와 매개 변수와 같이 쓰여 데이터 결과물의 생성에 기인하게 되는, 과정에 대한 설명(일련의 단계)입니다. 따라서, 출처의 구조는 주어진 결과물의 집합을 얻기 위해 사용되는 작업 흐름(또는 작업 흐름들)의 구조를 반영합니다.

In fact, a catalyst for the widespread use of workflow systems in science has been that they can be easily used to automatically capture provenance. While early workflow systems have been extended to capture provenance, VisTrails was designed to support provenance.

사실상, 학계에서의 작업 흐름 시스템의 사용을 확산시킨 촉매가 된 것은 작업 흐름 시스템이 출처를 자동으로 추적하기 쉽게 해 준다는 점이었습니다. 초기 작업 흐름 시스템들은 출처를 추적하기 위해 확장되었지만, VisTrails는 출처 추적을 염두에 두고 설계되었습니다.

![Figure 23.2: Provenance of Exploration Enhanced by Annotations](http://aosabook.org/images/vistrails/overview.png)

![그림 23.2: 주석으로 향상시킨 탐구 내용의 출처](http://aosabook.org/images/vistrails/overview.png)

### 23.1.3. User Interface and Basic Functionality

### 23.1.3. 사용자 인터페이스와 기본 기능

The different user interface components of the system are illustrated in Figure 23.1 and Figure 23.2. Users create and edit workflows using the Workflow Editor.

사용자 인터페이스의 구성 요소들이 그림 23.1과 그림 23.2에 표현되어 있습니다. 사용자들은 워크플로우 에디터를 통해 작업 흐름을 편집합니다.

To build the workflow graphs, users can drag modules from the Module Registry and drop them into the Workflow Editor canvas. VisTrails provides a series of built-in modules, and users can also add their own (see Section 23.3 for details). When a module is selected, VisTrails displays its parameters (in the Parameter Edits area) where the user can set and modify their values.

작업 흐름 그래프를 만들기 위해서, 사용자들은 모듈 레지스트리에서 모듈을 끌어 워크플로우 에디터 캔버스에 넣을 수 있습니다. VisTrails는 몇 가지 내장 모듈을 제공하며, 사용자들이 자신의 모듈을 추가할 수도 있습니다(23.3 에서 자세히 설명됩니다). 모듈이 선택되었을 때, VisTrails는 매개 변수 편집 영역에 사용자가 설정하고 편집할 수 있는, 모듈의 매개 변수들을 표시해 줍니다.

As a workflow specification is refined, the system captures the changes and presents them to the user in the Version Tree View described below. Users may interact with the workflows and their results in the VisTrails Spreadsheet. Each cell in the spreadsheet represents a view that corresponds to a workflow instance. In Figure 23.1, the results of the workflow shown in the Workflow Editor are displayed on the top-left cell of the spreadsheet. Users can directly modify the parameters of a workflow as well as synchronize parameters across different cells in the spreadsheet.

작업 흐름의 규칙이 다듬어짐과 동시에, VisTrails는 변경 사항을 추적하여, 아래에 설명된 버전 트리 뷰를 통해 사용자에게 변경 사항을 보여줍니다. 사용자들은 작업 흐름과 결과물을 VisTrails 스프레드시트를 통해 상호 작용할 수 있습니다. 스프레드시트의 각 셀은 작업 흐름의 인스턴스에 대응됩니다. 그림 23.1에서, 워크플로우 에디터에 나타나 있는 작업 흐름의 결과물들은 스프레드시트의 왼쪽 상단에 표시되어 있습니다. 사용자들은 작업 흐름의 매개 변수를 직접적으로 편집할 수 있으며, 스프레드시트 위의 여러 셀에 있는 매개 변수들을 동기화시킬 수도 있습니다.

The Version Tree View helps users to navigate through the different workflow versions. As shown in Figure 23.2, by clicking on a node in the version tree, users can view a workflow, its associated result (Visualization Preview), and metadata. Some of the metadata is automatically captured, e.g., the id of the user who created a particular workflow and the creation date, but users may also provide additional metadata, including a tag to identify the workflow and a written description.

버전 트리 뷰는 사용자들이 서로 다른 작업 흐름의 버전을 탐색할 수 있게 도와줍니다. 그림 23.2 처럼, 사용자들은 버전 트리의 노드를 클릭하여 작업 흐름과, 연관된 결과물(시각화 미리 보기), 그리고 메타데이터를 볼 수 있습니다. 특정 작업 흐름을 생성한 사용자의 id, 생성 날짜 등 몇몇 메타데이터는 자동적으로 추적되며, 작업 흐름을 식별하기 위한 태그나 설명 등, 사용자가 직접 추가적인 메타데이터를 제공할 수도 있습니다.

![Figure 23.3: VisTrails Architecture](http://aosabook.org/images/vistrails/system-interaction.png)

![Figure 23.3: VisTrails 설계도](http://aosabook.org/images/vistrails/system-interaction.png)

## 23.2. Project History

## 23.2. 프로젝트의 역사

Initial versions of versions of VisTrails were written in Java and C++ [BCC+05]. The C++ version was distributed to a few early adopters, whose feedback was instrumental in shaping our requirements for the system.

VisTrails의 초기 버전들은 Java와 C++로 작성되었습니다. C++ 버전은 소수의 얼리 어답터들에게 배포되었으며, 이를 통해 얻은 피드백은 VisTrails의 요구 사항을 정하는 데 주된 역할을 하였습니다.

Having observed a trend in the increase of the number of Python-based libraries and tools in multiple scientific communities, we opted to use Python as the basis for VisTrails. Python is quickly becoming a universal modern glue language for scientific software. Many libraries written in different languages such as Fortran, C, and C++ use Python bindings as a way to provide scripting capabilities. Since VisTrails aims to facilitate the orchestration of many different software libraries in workflows, a pure Python implementation makes this much easier. In particular, Python has dynamic code loading features similar to the ones seen in LISP environments, while having a much bigger developer community, and an extremely rich standard library. Late in 2005, we started the development of the current system using Python/PyQt/Qt. This choice has greatly simplified extensions to the system, in particular, the addition of new modules and packages.

여러 과학 커뮤니티 내에서 늘어나는 파이썬 기반 라이브러리와 도구의 추세를 관찰하여, VisTrails의 기반을 파이썬으로 작성하기로 선택하였습니다. 파이썬은 빠른 속도로 과학 소프트웨어를 위한, 보편적이고 현대적인 보조 언어로 거듭나고 있습니다. Fortran, C, C++ 등 다른 여러 언어로 작성된 라이브러리들이 스크립팅 기능을 제공하기 위해 파이썬 바인딩을 사용합니다. VisTrails가 작업 흐름에 다양한 소프트웨어 라이브러리를 묶어 사용할 수 있도록 하는 것을 목표로 하기 때문에, 순수 파이썬으로 구현체를 작성하는 것은 이러한 작업을 매우 쉽게 할 수 있게 합니다. 특히, 파이썬에는 LISP 환경과 비슷하게 동적으로 코드를 불러오는 기능, 훨씬 큰 개발자 커뮤니티, 그리고 풍부한 표준 라이브러리가 있습니다. 2005년 말, 우리는 Python/PyQt/Qt를 이용해 현재의 시스템을 개발하기 시작했습니다. 이러한 선택은 VisTrails의 확장, 특히 새로운 모듈과 패키지를 추가하는 것을 매우 간단히 할 수 있게 하였습니다.

A beta version of the VisTrails system was first released in January 2007. Since then, the system has been downloaded over twenty-five thousand times.

VisTrail의 베타 버전은 2007년 1월에 처음 공개되었습니다. 그 이래, VisTrails는 2만 5천 번 이상 다운로드 되었습니다.

## 23.3. Inside VisTrails

## 23.3. VisTrails의 내부

The internal components that support the user-interface functionality described above are depicted in the high-level architecture of VisTrails, shown in Figure 23.3. Workflow execution is controlled by the Execution Engine, which keeps track of invoked operations and their respective parameters and captures the provenance of workflow execution (Execution Provenance). As part of the execution, VisTrails also allows the caching of intermediate results both in memory and on disk. As we discuss in Section 23.3, only new combinations of modules and parameters are re-run, and these are executed by invoking the appropriate functions from the underlying libraries (e.g., matplotlib). Workflow results, connected to their provenance, can then be included in electronic documents (Section 23.4).

위에서 설명된 사용자 인터페이스 기능을 구현하는 내부 구성 요소는 그림 23.3에 있는 VisTrails의 고수준 설계에 표현되어 있습니다. 작업 흐름의 실행은, 실행된 명령들과 명령의 매개 변수들, 그리고 작업 흐름의 실행의 출처를 추적하는 실행 엔진에 의해 제어됩니다. VisTrails는 작업 흐름 실행의 일부로서 중간 결과물을 메모리와 디스크에 캐싱도 가능하게 합니다. 23.3장에서 설명되겠지만, 새로운 모듈과 매개 변수의 조합만이 다시 실행되며, 이러한 것들은 내재된 라이브러리(e.g., matplotlib)로부터의 함수를 호출함으로서 실행됩니다. 작업 흐름의 결과물들은, 출처와 연결 된 이후에 전자 문서(23.4 장)에 포함될 수 있습니다.

Information about changes to workflows is captured in a Version Tree, which can be persisted using different storage back ends, including an XML file store in a local directory and a relational database. VisTrails also provides a query engine that allows users to explore the provenance information.

작업 흐름에 대한 변경 사항의 정보는 버전 트리에서 추적되며, 로컬 디렉토리의 XML 파일, 관계형 데이터베이스 등 여러 스토리지 백엔드를 사용하여 영구 저장할 수 있습니다. VisTrails는 사용자들이 출처 정보를 탐색할 수 있도록 쿼리 엔진도 제공합니다.

We note that, although VisTrails was designed as an interactive tool, it can also be used in server mode. Once workflows are created, they can be executed by a VisTrails server. This feature is useful in a number of scenarios, including the creation of Web-based interfaces that allows users to interact with workflows and the ability to run workflows in high-performance computing environments.

VisTrails는 대화식 도구로서 설계되었지만, 서버 모드로도 사용될 수 있습니다. 작업 흐름은 생성된 이후, VisTrails 서버에 의해 실행될 수 있습니다. 이 기능은, 웹 기반 인터페이스를 만들고 이를 통해 사용자들이 작업 흐름과 상호 작용하거나, 고성능 컴퓨팅 환경에서 작업 흐름을 실행하는 등 몇몇 상황에서 유용하게 사용될 수 있습니다.

### 23.3.1. The Version Tree: Change-Based Provenance

### 23.3.1. 버전 트리: 변경점 기반 출처

![Figure 23.4: Change-Based Provenance Model](http://aosabook.org/images/vistrails/change-based-prov.png)

![Figure 23.4: 변경점 기반 출처 모델](http://aosabook.org/images/vistrails/change-based-prov.png)

A new concept we introduced with VisTrails is the notion of provenance of workflow evolution [FSC+06]. In contrast to previous workflow and workflow-based visualization systems, which maintain provenance only for derived data products, VisTrails treats the workflows as first-class data items and also captures their provenance. The availability of workflow-evolution provenance supports reflective reasoning. Users can explore multiple chains of reasoning without losing any results, and because the system stores intermediate results, users can reason about and make inferences from this information. It also enables a series of operations which simplify exploratory processes. For example, users can easily navigate through the space of workflows created for a given task, visually compare the workflows and their results (see Figure 23.4), and explore (large) parameter spaces. In addition, users can query the provenance information and learn by example.

우리는 VisTrails에서 작업 흐름 변화의 출처 개념을 새롭게 도입했습니다. 파생된 데이터에 대한 출처만 유지하는 이전 작업 흐름과 작업 흐름 기반 시각화 시스템과 대비하여, VisTrails는 작업 흐름 역시 데이터 항목으로 취급하며, 이에 대한 출처도 추적합니다. 작업 흐름 변화에 대한 출처 정보를 가지기 때문에, 반성적 사고를 할 수 있도록 도와줍니다. 사용자들은 결과물을 잃지 않으면서 여러 논리적 구조를 탐색할 수 있으며, VisTrails는 중간 결과물을 저장하기 때문에, 이러한 정보를 이용해서 증명, 추론할 수 있습니다. 이는 탐구 과정을 단순화시킬 수 있는 일련의 작업들을 가능하게 하기도 합니다. 예를 들어, 사용자들은 주어진 작업에 대해 생성된 작업 흐름 공간의 탐색, 작업 흐름과 그 결과를 시각적으로 비교(그림 23.4), 매개 변수 영역을 탐색하는 등의 작업을 쉽게 할 수 있습니다. 또, 출처 정보를 조회하여 예시를 통해 학습할 수도 있습니다.

The workflow evolution is captured using the change-based provenance model. As illustrated in Figure 23.4, VisTrails stores the operations or changes that are applied to workflows (e.g., the addition of a module, the modification of a parameter, etc.), akin to a database transaction log. This information is modeled as a tree, where each node corresponds to a workflow version, and an edge between a parent and a child node represents the change applied to the parent to obtain the child. We use the terms version tree and vistrail (short for visual trail) interchangeably to refer to this tree. Note that the change-based model uniformly captures both changes to parameter values and to workflow definitions. This sequence of changes is sufficient to determine the provenance of data products and it also captures information about how a workflow evolves over time. The model is both simple and compact—it uses substantially less space than the alternative of storing multiple versions of a workflow.

작업 흐름의 변화는 변경점 기반의 출처 모델을 사용하여 추적됩니다. 그림 23.4에 나타난 것 처럼, VisTrails는 작업 흐름에 적용된 작업이나 변경점(e.g., 모듈의 추가, 매개 변수의 수정, etc.)을 데이터베이스 트랜잭션 기록과 유사하게 저장합니다. 이 정보는 각 노드가 작업 흐름의 버전에 대응되고, 부모와 자식 노드간의 변을 자식을 얻기 위해 부모에 반영된 변경점에 대응되는 트리 구조로 모델링 됩니다. 우리는 이 트리를 버전 트리 또는 vistrail(visual trail의 줄임말)이라고 부릅니다. 변경점 기반의 모델이 매개 변수 값과 작업 흐름의 정의를 균일하게 추적한다는 점을 보면, 이 일련의 변경점들이 데이터 결과물의 출처를 결정짓기에 충분하고, 작업 흐름이 시간이 지나며 어떻게 변해왔는지 추적한다는 것을 알 수 있습니다. 이 모델은 간단하면서도 효율적입니다. 여러 버전의 작업 흐름을 저장하는 것에 비해 상당히 적은 공간을 사용합니다.

There are a number of benefits that come from the use of this model. Figure 23.4 shows the visual difference functionality that VisTrails provides for comparing two workflows. Although the workflows are represented as graphs, using the change-based model, comparing two workflows becomes very simple: it suffices to navigate the version tree and identify the series of actions required to transform one workflow into the other.

이러한 모델을 사용함으로서 얻는 몇 가지 이점들이 있습니다. 그림 23.4는 VisTrail이 두 작업 흐름을 비교하기 위해 제공하는 시각적 변경점 기능을 보여줍니다. 작업 흐름들이 그래프로 표현되어 있지만, 변경점 기반 모델을 사용하기 때문에 두 작업 흐름의 비교가 매우 쉬워집니다. 버전 트리를 탐색하며 하나의 작업 흐름이 다른 작업 흐름으로 변하는 데 필요한 일련의 작업들을 확인하는 것으로 충분합니다.

Another important benefit of the change-based provenance model is that the underlying version tree can serve as a mechanism to support collaboration. Because designing workflows is a notoriously difficult task, it often requires multiple users to collaborate. Not only does the version tree provide an intuitive way to visualize the contribution of different users (e.g., by coloring nodes according to the user who created the corresponding workflow), but the monotonicity of the model allows for simple algorithms for synchronizing changes performed by multiple users.

변경점 기반 모델의 또 다른 중요한 이점은, 기반이 되는 버전 트리가 협업을 위한 체계로서 사용될 수 있다는 것입니다. 작업 흐름을 설계하는 일은 어려운 작업으로 악명이 높아, 여러 사용자가 협업하도록 요구합니다. 버전 트리가 서로 다른 사용자들의 기여를 시각화하기에 직관적인 방식을 제공할 뿐만이 아니라(e.g., 해당 작업 흐름을 작성한 사용자에 따라 노드에 색을 칠함), 모델의 단조로움이 단순한 알고리즘만으로도 변경점을 여러 사용자간 동기화할 수 있게 해줍니다. 

Provenance information can be easily captured while a workflow is being executed. Once the execution completes, it is also important to maintain strong links between a data product and its provenance, i.e., the workflow, parameters and input files used to derive the data product. When data files or provenance are moved or modified, it can be difficult to find the data associated with the provenance or to find the provenance associated with the data. VisTrails provides a persistent storage mechanism that manages input, intermediate, and output data files, strengthening the links between provenance and data. This mechanism provides better support for reproducibility because it ensures the data referenced in provenance information can be readily (and correctly) located. Another important benefit of such management is that it allows caching of intermediate data which can then be shared with other users.

출처 정보는 작업 흐름이 실행되는 중에 쉽게 추적될 수 있습니다. 실행이 완료된 후, 데이터 결과물과 그 출처, 즉, 데이터 결과물을 기인한 작업 흐름, 매개 변수, 그리고 입력 파일들과의 강한 관계을 유지하는 것 역시 중요합니다. 데이터 파일이나 출처가 옮겨졌거나 편집되었을 때, 그 출처와 연관된 데이터나 데이터와 연관된 출처를 찾기가 어려워질 수 있습니다. VisTrails는 입력, 중간 데이터, 그리고 출력 데이터 파일을 영속적으로 저장하는 체계를 제공하여 출처와 데이터의 관계를 강하게 유지할 수 있게 합니다. 이 체계는 출처 정보에 언급된 데이터를 쉽고 정확하게 찾을 수 있게 하기 때문에 재현성을 강화합니다. 이러한 관리 방식은, 중간 데이터를 캐싱하여 다른 사용자들과 공유할 수 있게 해준다는 점에서도 중요한 잇점을 가집니다. 

### 23.3.2. Workflow Execution and Caching

### 23.3.2. 작업 흐름 실행과 캐싱

The execution engine in VisTrails was designed to allow the integration of new and existing tools and libraries. We tried to accommodate different styles commonly used for wrapping third-party scientific visualization and computation software. In particular, VisTrails can be integrated with application libraries that exist either as pre-compiled binaries that are executed on a shell and use files as input/outputs, or as C++/Java/Python class libraries that pass internal objects as input/output.

VisTrails의 실행 엔진은 기존 및 새로운 도구와 라이브러리와 접목될 수 있게 설계되었습니다. 우리는 써드 파티 과학적 시각화 및 계산 소프트웨어를 래핑하는 여러 다른 보편적인 방식들을 수용하려고 하였습니다. VisTrails는 특히, 입력 및 출력을 파일로 받는 컴파일된 바이너리나, 내부 객체로 받는 C++/Java/Python 클래스 형태의 어플리케이션 라이브러리와 접목될 수 있습니다.

VisTrails adopts a dataflow execution model, where each module performs a computation and the data produced by a module flows through the connections that exist between modules. Modules are executed in a bottom-up fashion; each input is generated on-demand by recursively executing upstream modules (we say module A is upstream of B when there is a sequence of connections that goes from A to B). The intermediate data is temporarily stored either in memory (as a Python object) or on disk (wrapped by a Python object that contains information on accessing the data).

VisTrails는, 각 모듈이 계산을 하여 생성된 데이터가 모듈 간 존재하는 연결을 통해 흐르는 모듈 데이터 흐름 실행 모델을 도입하였습니다. 모듈들은 상향 방식으로 실행됩니다. 각 입력은 필요할 때 마다 업스트림 모듈을 재귀적으로 실행하여(모듈 A에서 B로 가는 일련의 연결이 있을 때 모듈 A가 모듈 B의 업스트림이라고 부릅니다) 생성됩니다. 중간 데이터는 메모리(파이썬 객체의 형식으로) 또는 디스크(데이터에 접근 할 수 있게 하는 정보를 포함한 파이썬 객체로 래핑된 형식으로)에 임시로 저장됩니다.

To allow users to add their own functionality to VisTrails, we built an extensible package system (see Section 23.3). Packages allow users to include their own or third-party modules in VisTrails workflows. A package developer must identify a set of computational modules and for each, identify the input and output ports as well as define the computation. For existing libraries, a compute method needs to specify the translation from input ports to parameters for the existing function and the mapping from result values to output ports.

사용자들이 VisTrails에 직접 기능을 추가할 수 있도록, 우리는 확장 가능한 패키지 시스템(23.3장에서 자세히 설명됩니다)을 만들었습니다. 패키지는 사용자들이 사용자의 모듈이나 써드 파티 모듈을 VisTrails 작업 흐름에 추가할 수 있게 합니다. 패키지 개발자는 계산 모듈을 명시하고, 각 모듈에 대한 입력과 출력 포트를 명시하고 계산을 정의해야 합니다. 존재하는 라이브러리에 대해서 계산 메서드는, 입력 포트로부터 존재하는 함수의 매개 변수로의 번역과, 결과 값으로부터 출력 포트로의 매핑을 명시해야 합니다.

In exploratory tasks, similar workflows, which share common sub-structures, are often executed in close succession. To improve the efficiency of workflow execution, VisTrails caches intermediate results to minimize recomputation. Because we reuse previous execution results, we implicitly assume that cacheable modules are functional: given the same inputs, modules will produce the same outputs. This requirement imposes definite behavior restrictions on classes, but we believe they are reasonable.

탐구 작업에서, 공통의 하부 구조를 가지는 비슷한 작업 흐름들은, 주로 잇달아 실행됩니다. 작업 흐름 실행의 효율성을 높이기위해, VisTrails는 중간 결과를 캐싱하여 재계산을 최소화합니다. 이전 실행 결과를 재활용하기 때문에, 캐시 가능한 모듈은 함수적, 즉, 같은 입력이 주어지면, 같은 출력을 생성한다고 암시적으로 가정합니다. 이 요구 사항은 클래스에 확정적인 동작이라는 제한을 걸지만, 우리는 이것이 합리적이라고 생각합니다.

There are, however, obvious situations where this behavior is unattainable. For example, a module that uploads a file to a remote server or saves a file to disk has a significant side effect while its output is relatively unimportant. Other modules might use randomization, and their non-determinism might be desirable; such modules can be flagged as non-cacheable. However, some modules that are not naturally functional can be converted; a function that writes data to two files might be wrapped to output the contents of the files.

하지만, 이런 동작을 요구할 수 없는 상황들도 있습니다. 예를 들어, 파일을 원격 서버로 업로드하거나, 파일을 디스크에 저장하는 모듈의 출력은 비교적 중요하지 않지만, 큰 부작용을 가져올 수 있습니다. 어떤 모듈들은 무작위수를 사용하고 비결정성이 바람직한 동작일 수 있습니다. 이러한 모듈들은 캐시 불가능한 것으로 표시할 수 있습니다. 하지만, 어떤 함수적이지 않은 모듈들은 함수적이도록 변환할 수 있습니다. 두 파일에 데이터를 쓰는 함수는 파일들의 내용을 반환하도록 래핑될 수 있습니다.

### 23.3.3. Data Serialization and Storage

### 23.3.3. 데이터의 직렬화와 저장

One of the key components of any system supporting provenance is the serialization and storage of data. VisTrails originally stored data in XML via simple fromXML and toXML methods embedded in its internal objects (e.g., the version tree, each module). To support the evolution of the schema of these objects, these functions encoded any translation between schema versions as well. As the project progressed, our user base grew, and we decided to support different serializations, including relational stores. In addition, as schema objects evolved, we needed to maintain better infrastructure for common data management concerns like versioning schemas, translating between versions, and supporting entity relationships. To do so, we added a new database (db) layer.

출처를 지원하는 시스템의 핵심 구성 요소는 데이터의 직렬화와 저장입니다. VisTrails는 처음에 데이터를 단순히 내부 객체(e.g., 버전 트리, 모듈)에 정의된 fromXML과 toXML 메서드를 통해 XML로 저장하였습니다. 이런 객체들의 스키마가 변하는 것을 지원하기 위해, 이 메서드들은 스키마 버전 간의 번역도 직렬화하였습니다. 프로젝트가 발전하며, 사용자층이 성장하였고, 우리는 관계형 저장소 등 다른 직렬화 방식을 지원할 필요가 생겼습니다. 또, 스키마 객체가 변하면서 스키마 버전 관리, 버전 간의 번역, 개체 간 관계의 지원 같은 공통적인 데이터 관리 문제를 개선해야 했으며, 이를 위해 데이터베이스(db) 층을 추가하였습니다.

The db layer is composed of three core components: the domain objects, the service logic, and the persistence methods. The domain and persistence components are versioned so that each schema version has its own set of classes. This way, we maintain code to read each version of the schema. There are also classes that define translations for objects from one schema version to those of another. The service classes provide methods to interface with data and deal with detection and translation of schema versions.

데이터베이스 층은, 도메인 객체, 서비스 로직, 그리고 영속 메서드의 세 가지 핵심 구성 요소로 이루어져 있습니다. 도메인과 영속성 부분은 각 스키마 버전이 각작의 클래스를 가질 수 있도록 버전 관리 되어 있습니다. 이 방식을 통해 서로 다른 버전의 스키마를 읽기 위한 코드를 유지할 수 있습니다. 하나의 스키마 버전에서 다른 버전의 스키마로의 번역을 제공하는 메서드를 정의하는 클래스도 있습니다. 서비스 클래스는 데이터를 다루고, 스키마 버전이 바뀌는 것을 탐지하고 버전 간 번역을 위한 메서드를 제공합니다.

Because writing much of this code is tedious and repetitive, we use templates and a meta-schema to define both the object layout (and any in-memory indices) and the serialization code. The meta-schema is written in XML, and is extensible in that serializations other than the default XML and relational mappings VisTrails defines can be added. This is similar to object-relational mappings and frameworks like Hibernate2 and SQLObject3, but adds some special routines to automate tasks like re-mapping identifiers and translating objects from one schema version to the next. In addition, we can also use the same meta-schema to generate serialization code for many languages. After originally writing meta-Python, where the domain and persistence code was generated by running Python code with variables obtained from the meta-schema, we have recently migrated to Mako templates4.

이런 코드를 작성하는 일은 장황하고 반복적이기 때문에, 객체 레이아웃(메모리 첨자도 포함하는)과 직렬화 코드를 정의하는 데 템플릿과 메타 스키마를 사용합니다. 메타 스키마는 XML로 작성되어 있으며, 기본 XML 직렬화나 VisTrails에 의해 정의된 관계형 매핑 외 다른 직렬화 방식을 더할 수 있어 확장 가능합니다. 이것은 Hibernate2나 SQLObject3같은 객체 관계형 매핑이나 프레임워크와 비슷하지만, 식별자 재할당이나 객체 버전 간 번역을 위한 루틴들을 더합니다. 또, 같은 메타 스키마를 사용해 여러 언어에 대한 직렬화 코드를 생성할 수 있습니다. 초기에는 메타 스키마로부터 가져온 변수로 파이썬 코드를 실행하여 도메인과 영속성 코드를 생성했던 메타-파이썬으로 작성을 하다가, 최근에는 Mako 템플릿으로 이전하였습니다.

Automatic translation is key for users that need to migrate their data to newer versions of the system. Our design adds hooks to make this translation slightly less painful for developers. Because we maintain a copy of code for each version, the translation code just needs to map one version to another. At the root level, we define a map to identify how any version can be transformed to any other. For distant versions, this usually involves a chain through multiple intermediate versions. Initially, this was a forward-only map, meaning new versions could not be translated to old versions, but reverse mappings have been added for more-recent schema mappings.

자동 번역은 사용자들의 데이터를 새로운 버전의 VisTrails로 이전하기 위해 필수적입니다. 우리 설계는 개발자들이 이러한 번역을 쉽게 구현할 수 있도록 몇가지 훅을 제공합니다. 각 버전에 대한 코드를 보존하기 때문에, 번역 코드는 단지 버전 간 매핑만 하면 됩니다. 최하위단에서 어떠한 하나의 버전을 어떠한 다른 버전으로 변화시킬 수 있는 매핑을 정의합니다. 거리가 먼 버전 간에는 다수의 중간 버전을 거칩니다. 초기에 이 매핑은 정방향, 즉 새로운 버전이 이전 버전으로는 번역될 수 없는 매핑이었지만, 최근의 스키마 매핑에서는 역방향 매핑도 추가되었습니다.

Each object has an update_version method that takes a different version of an object and returns the current version. By default, it does a recursive translation where each object is upgraded by mapping fields of the old object to those in a new version. This mapping defaults to copying each field to one with the same name, but it is possible to define a method to "override" the default behavior for any field. An override is a method that takes the old object and returns a new version. Because most changes to the schema only affect a small number of fields, the default mappings cover most cases, but the overrides provide a flexible means for defining local changes.

각 객체는 서로 다른 버전의 객체를 받아 현재 버전을 반환하는 update_version 메서드를 가지고 있습니다. 기본값으로, 각 객체가 이전 객체의 필드를 새로운 버전의 객체로 매핑되는 방식으로 업그레이드되는 재귀적 번역을 합니다. 이 매핑은 기본값으로 같은 이름을 가진 필드는 복사하지만, 이런 동작을 오버라이드 할 수 있는 메서드를 정의할 수도 있습니다. 오버라이드는 이전 객체를 받아 새로운 객체를 반환하는 메서드입니다. 스키마에 대한 대부분의 변경점은 소수의 필드에만 영향을 미치기 때문에 기본 매핑이 대부분의 상황을 처리할 수 있지만, 오버라이드는 국소적인 변경점을 정의할 수 있는 유연한 방식을 제공합니다.

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

Python classes can be defined dynamically via function calls to the type callable. The return value is a representation of a class that can be used in exactly the same way that a typically-defined Python class can. Python modules can be imported via function calls to __import__, and the resulting value behaves in the same way as the identifier in a standard import statement. The path from which these modules come from can also be specified at runtime.

파이썬 클래스는 호출 가능한 타입으로의 함수 호출을 통해 동적으로 정의할 수 있습니다. 반환값은 클래스의 표현형이며, 전형적으로 정의된 파이썬 클래스와 같은 방식으로 사용할 수 있습니다. 파이썬 모듈은 __import__으로의 함수 호출로 들여올 수 있으며, 반환값은 표준 import 선언문의 식별자와 같은 방식으로 작동합니다. 모듈들을 찾을 위치 또한 런타임에서 정의할 수 있습니다.

Using Python as our target has a few disadvantages, of course. First of all, this dynamic nature of Python means that while we would like to ensure some things like type safety of VisTrails packages, this is in general not possible. More importantly, some of the requirements for VisTrails modules, notably the ones regarding referential transparency (more on that later) cannot be enforced in Python. Still, we believe that it is worthwhile to restrict the allowed constructs in Python via cultural mechanisms, and with this caveat, Python is an extremely attractive language for software extensibility.

파이썬을 타겟으로 사용하는 것에는 몇 가지 단점도 있습니다. 먼저, 파이썬의 동적인 성질은, VisTrails 패키지의 타입 안정성을 보장하고 싶지만 그럴 수 없다는 것을 의미합니다. 더욱 중요한 것은, VisTrails 모듈에 대한 요구 사항, 특히 관계의 투명성(이후에 자세히 설명됩니다)에 대한 요구 사항은 파이썬을 사용하였을 때 강제할 수 없다는 것입니다. 그래도, 우리는 문화적 체계를 통해 파이썬에서 허용하는 구조를 제한하는 것이 할 만 하다고 생각하며, 이 체계에 대해서 유의한다면 파이썬은 소프트웨어 확장에 대해서는 아주 매력적인 언어라고 생각합니다.

### 23.3.5. VisTrails Packages and Bundles

### 23.3.5. VisTrails 패키지와 번들

A VisTrails package encapsulates a set of modules. Its most common representation in disk is the same representation as a Python package (in a possibly unfortunate naming clash). A Python package consists of a set of Python files which define Python values such as functions and classes. A VisTrails package is a Python package that respects a particular interface. It has files that define specific functions and variables. In its simplest form, a VisTrails package should be a directory containing two files: __init__.py and init.py.

VisTrails 패키지는 모듈들의 집합을 포함합니다. 디스크에 있는 VisTrails 패키지의 가장 흔한 형태는 파이썬 패키지의 형태(안타깝지만 때로는 이름이 겹치는)와 같습니다. 파이썬 패키지는 함수나 클래스 등의 값을 정의하는 파이썬 파일들의 집합으로 이루어져 있습니다. VisTrails 패키지는 특정 인터페이스를 구현하는 파이썬 패키지입니다. 특정한 함수와 변수를 정의하는 파일을 포함하고 있습니다. 가장 단순한 VisTrails 패키지는 __init__.py 파일과 init.py를 포함하는 폴더입니다. 

The first file __init__.py is a requirement of Python packages, and should only contain a few definitions which should be constant. Although there is no way to guarantee that this is the case, VisTrails packages failing to obey this are considered buggy. The values defined in the file include a globally unique identifier for the package which is used to distinguish modules when workflows are serialized, and package versions (package versions become important when handling workflow and package upgrades, see Section 23.4). This file can also include functions called package_dependencies and package_requirements. Since we allow VisTrails modules to subclass from other VisTrails modules beside the root Module class, it is conceivable for one VisTrails package to extend the behavior of another, and so one package needs to be initialized before another. These inter-package dependencies are specified by package_dependencies. The package_requirements function, on the other hand, specifies system-level library requirements which VisTrails, in some cases, can try to automatically satisfy, through its bundle abstraction.

첫번째 파일인 __init__.py는 파이썬 패키지의 요구 사항으로, 소수의 정적 정의만 해야 합니다. 이를 보장할 수는 없지만, 이를 따르지 않는 VisTrails 패키지는 버그가 있는 것으로 간주됩니다. 이 파일에는 패키지에 대한 고유 식별자와 패키지 버전(작업 흐름과 패키지 업그레이드를 다룰 때 버전은 중요한 정보입니다. 23.4장에 자세히 설명되어 있습니다)이 정의되어 있습니다. 이 파일은 package_dependencies와 package_requirements 함수를 포함할 수도 있습니다. VisTrails 모듈은 root 모듈 클래스 외에도 다른 VisTrails 모듈을 상속받을 수 있으므로, VisTrails 패키지가 다른 패키지의 기능을 확장하는 것도 있을 수 있는 일이며, 따라서 해당 패키지는 다른 패키지보다 먼저 초기화되어야 합니다. 이러한 패키지간의 의존성은 package_dependencies에 정의됩니다. 반면, package_requirements 함수는 시스템 레벨 라이브러리 종속성을 정의하며, VisTrails는 이러한 종속성들을 번들 추상화를 통해 종종 자동으로 충족시킬 수 있습니다.

A bundle is a system-level package that VisTrails manages via system-specific tools such as RedHat's RPM or Ubuntu's APT. When these properties are satisfied, VisTrails can determine the package properties by directly importing the Python module and accessing the appropriate variables.

번들은 VisTrails가 RedHat의 RPM이나 Ubuntu의 APT처럼 시스템 종속적인 도구를 통해 관리하는 시스템 레벨 패키지입니다. 이러한 속성을 만족시킬 때, VisTrails는 파이썬 모듈을 직접 임포트하여 필요한 변수들을 접근함으로서 패키지의 속성을 판단할 수 있습니다.

The second file, init.py, contains the entry points for all the actual VisTrails module definitions. The most important feature of this file is the definition of two functions, initialize and finalize. The initialize function is called when a package is enabled, after all the dependent packages have themselves been enabled. It performs setup tasks for all of the modules in a package. The finalize function, on the other hand, is usually used to release runtime resources (for example, temporary files created by the package can be cleaned up).

두번째 파일인 init.py는 실제 VisTrails 모듈 정의의 진입점을 포함합니다. 이 파일의 가장 중요한 특징은, initialize와 finalize 두 함수의 정의입니다. initialize 함수는 패키지가 활성화 될 때 의존 패키지들이 모두 활성화 된 후 호출되며, 패키지 안의 모든 모듈들에 대한 구성 작업을 실행합니다. finalize 함수는 런타임 자원(패키지가 생성한 임시 파일 등)을 할당 해재할 때 사용됩니다.

Each VisTrails module is represented in a package by one Python class. To register this class in VisTrails, a package developer calls the add_module function once for each VisTrails module. These VisTrails modules can be arbitrary Python classes, but they must respect a few requirements. The first of these is that each must be a subclass of a basic Python class defined by VisTrails called, perhaps boringly, Module. VisTrails modules can use multiple inheritance, but only one of the classes should be a VisTrails module—no diamond hierarchies in the VisTrails module tree are allowed. Multiple inheritance becomes useful in particular to define class mix-ins: simple behaviors encoded by parent classes which can be composed together to create more complicated behaviors.

각 VisTrails 모듈은 패키지 안의 하나의 파이썬 클래스에 의해 대표됩니다. 이 클래스를 VisTrails에 등록하기 위해서 패키지 개발자는 VisTrails 모듈 마다 add_module 함수를 호출합니다. 이 VisTrails 모듈들은 임의의 파이썬 클래스이지만, 몇 가지 요구 사항을 충족해야 합니다. 첫번째 요구사항은, VisTrails가 정의하는, 재미 없을지도 모르겠지만, Module이라고 불리는 기초 파이썬 클래스를 상속해야 한다는 것입니다. VisTrails 모듈은 다중 상속을 사용할 수 있지만, 하나의 클래스만이 VisTrails 모듈이어야 합니다. VisTrails 모듈 트리에서는 다이아몬드 계층을 허용하지 않습니다. 다중 상속은 클래스 믹스인을 정의할 때 유용합니다. 단순한 동작을 가지는 부모 클래스들을 함께 구성하여 복잡한 작업을 할 수 있습니다.

The set of available ports determine the interface of a VisTrails module, and so impact not only the display of these modules but also their connectivity to other modules. These ports, then, must be explicitly described to the VisTrails infrastructure. This can be done either by making appropriate calls to add_input_port and add_output_port during the call to initialize, or by specifying the per-class lists _input_ports and _output_ports for each VisTrails module.

사용 가능한 포트의 집합은 VisTrails 모듈의 인터페이스를 정의하며, 모듈의 표시 뿐만이 아니라 다른 모듈로의 연결성에도 영향을 미치게 됩니다. 이 포트들은 VisTrails에 명시적으로 알려져야 합니다. 이 작업은 initialize를 호출하는 중에 add_input_port와 add_output_port을 호출하거나, 각 VisTrails 모듈 마다 클래스에 _input_ports와 _output_ports 리스트를 정의함으로서 할 수 있습니다.

Each module specifies the computation to be performed by overriding the compute method. Data is passed between modules through ports, and accessed through the get_input_from_port and set_result methods. In traditional dataflow environments, execution order is specified on-demand by the data requests. In our case, the execution order is specified by the topological sorting of the workflow modules. Since the caching algorithm requires an acyclic graph, we schedule the execution in reverse topological sorted order, so the calls to these functions do not trigger executions of upstream modules. We made this decision deliberately: it makes it simpler to consider the behavior of each module separately from all the others, which makes our caching strategy simpler and more robust.

각 모듈은 compute 메서드를 오버라이딩하여 수행할 계산을 정의합니다. 데이터는 포트를 통해 모듈 간 전달되며, get_input_from_port와 set_result 메서드를 통해 접근됩니다. 전통적인 데이터 흐름 환경에서 실행 순서는 데이터 요청에 의해 필요에 따라 결정되지만, VisTrails의 경우 작업 흐름 모듈의 위상순서에 따라 결정됩니다. 캐싱 알고리즘이 비순환적 그래프를 요구하므로, 우리는 함수 호출이 업스트림 모듈의 실행을 야기하지 않도록 실행 순서를 역위상순으로 정렬하여 스케쥴링합니다. 우리는 이 결정을 고의로 내렸으며, 각 모듈의 동작을 단독으로 고려하기 간편해지고, 캐싱 전략을 간단하고 견고하게 만들 수 있었습니다.

As a general guideline, VisTrails modules should refrain from using functions with side-effects during the evaluation of the compute method. As discussed in Section 23.3, this requirement makes caching of partial workflow runs possible: if a module respects this property, then its behavior is a function of the outputs of upstream modules. Every acyclic subgraph then only needs to be computed once, and the results can be reused.

일반적인 지침으로, VisTrails 모듈은 compute 메서드의 실행 중에 부작용을 가지는 함수의 사용을 삼가야 합니다. 23.3장에서 언급했던 것처럼, 이 요구사항은 부분적인 작업 흐름의 실행의 캐싱을 가능하게 합니다. 모듈이 이 속성을 존중한다면, 해당 모듈의 동작은 업스트림 모듈의 결과물에 함수적입니다. 따라서 모든 비순환식 부분 그래프는 한 번만 계산되면 되고, 결과물을 재사용할 수 있게 됩니다.

### 23.3.6. Passing Data as Modules

### 23.3.6. 데이터를 모듈로서 전달하기

One peculiar feature of VisTrails modules and their communication is that the data that is passed between VisTrails modules are themselves VisTrails modules. In VisTrails, there is a single hierarchy for module and data classes. For example, a module can provide itself as an output of a computation (and, in fact, every module provides a default "self" output port). The main disadvantage is the loss of conceptual separation between computation and data that is sometimes seen in dataflow-based architectures. There are, however, two big advantages. The first is that this closely mimics the object type systems of Java and C++, and the choice was not accidental: it was very important for us to support automatic wrapping of large class libraries such as VTK. These libraries allow objects to produce other objects as computational results, making a wrapping that distinguishes between computation and data more complicated.

VisTrails 모듈과 모듈간 통신의 특이한 점은, 모듈 간 전달되는 데이터 자체도 VisTrails 모듈이라는 점입니다. VisTrails에는 모듈과 데이터 클래스 위한 하나의 계층이 있습니다. 예를 들어, 모듈은 계산의 결과로 자기 자신을 제공할 수 있습니다(사실, 모든 모듈은 기본값으로 "self" 출력 포트를 제공합니다). 이것이 주된 단점은, 데이터 흐름 기반 설계에서 가끔 보이는, 계산과 데이터의 개념적인 분리의 상실을 야기한다는 점입니다. 하지만 두 가지 큰 장점을 얻을 수 있습니다. 첫번째는 이러한 

The second advantage this decision brings is that defining constant values and user-settable parameters in workflows becomes easier and more uniformly integrated with the rest of the system. Consider, for example, a workflow that loads a file from a location on the Web specified by a constant. This is currently specified by a GUI in which the URL can be specified as a parameter (see the Parameter Edits area in Figure 23.1). A natural modification of this workflow is to use it to fetch a URL that is computed somewhere upstream. We would like the rest of the workflow to change as little as possible. By assuming modules can output themselves, we can simply connect a string with the right value to the port corresponding to the parameter. Since the output of a constant evaluates to itself, the behavior is exactly the same as if the value had actually been specified as a constant.

이 결정의 두번째 장점은, 상수와, 사용자가 설정 가능한 매개 변수를 작업 흐름 내에서 정의하기 더 쉽고 시스템의 다른 부분과도 균일하게 통합된다는 것입니다. 상수로 정의된 웹 위치로부터 파일을 불러오는 작업 흐름을 예로 들면, URL은 매개 변수로서 GUI를 통해 지정됩니다(그림 23.1의 매개 변수 편집 영역). 이 작업 흐름을 조금 더 자연스럽게 편집을 가하자면, URL을 업스트림의 다른 곳에서 계산하여 가져 오는 것입니다. 모듈들이 자기 자신을 결과로 제공할 수 있다고 가정하여, 단지 파라미터에 해당되는 포트에 문자열을 연결하면 됩니다. 상수의 출력은 상수 자기 자신이기 때문에, 이것은 값이 상수로 지정되었을 때와 똑같이 작동합니다.

![Figure 23.5: Prototyping New Functionality with the PythonSource Module](http://aosabook.org/images/vistrails/python-source.png)

![그림 23.5: PythonSource 모듈으로 새로운 기능 프로토타이핑 하기](http://aosabook.org/images/vistrails/python-source.png)

There are other considerations involved in designing constants. Each constant type has a different ideal GUI interface for specifying values. For example, in VisTrails, a file constant module provides a file chooser dialog; a Boolean value is specified by a checkbox; a color value has a color picker native to each operating system. To achieve this generality, a developer must subclass a custom constant from the Constant base class and provide overrides which define an appropriate GUI widget and a string representation (so that arbitrary constants can be serialized to disk).

상수들을 설계하는 데 고려해야 할 다른 점들도 있습니다. 상수형마다 다른 값을 설정하기 위한 이상적인 GUI 인터페이스를 가집니다. 예를 들어, VisTrails에서는, 파일 상수 모듈은 파일 선택 대화 창을 제공하고, 불린 값은 체크박스로 표현되며, 색 값은 운영체제에 따른 색 선택 창을 가집니다. 이러한 일반성을 가지기 위해, 개발자는 Constant 기반 클래스를 상속하고, 적절한 GUI 위젯을 정의하는 오버라이드를 제공하고, 문자열 표현형을 정의해야 합니다(임의의 상수들이 디스크에 직렬화될 수 있도록). 

We note that, for simple prototyping tasks, VisTrails provides a built-in PythonSource module. A PythonSource module can be used to directly insert scripts into a workflow. The configuration window for PythonSource (see Figure 23.5) allows multiple input and output ports to be specified along with the Python code that is to be executed.

단순한 프로토타이핑 작업에 대해서는, VisTrails는 내장된 PythonSource 모듈을 제공합니다. PythonSource 모듈은 작업 흐름에 스크립트를 직접 삽입하는데 쓰일 수 있습니다. PythonSource(그림 23.5)의 설정 창은 다수의 입력과 출력 포트와 함께 실행될 파이썬 코드의 입력을 지원합니다.

## 23.4. Components and Features

## 23.4. 구성 요소와 기능

As discussed above, VisTrails provides a set of functionalities and user interfaces that simplify the creation and execution of exploratory computational tasks. Below, we describe some of these. We also briefly discuss how VisTrails is being used as the basis for an infrastructure that supports the creation of provenance-rich publications. For a more comprehensive description of VisTrails and its features, see VisTrails' online documentation6.

위에서 설명된 것처럼, VisTrails는 탐구적 계산 작업의 제작과 실행을 간편하게 해주는 기능들의 집합과 사용자 인터페이스를 제공합니다. 아래에서 이에 대한 설명을 합니다. VisTrails가 어떻게 출처 정보가 풍부한 발행물을 만드는 기반으로서 사용되는지 설명합니다. VisTrails에 대한 더욱 자세한 기능과 설명은 온라인 문서에 있습니다.

![Figure 23.6: The Visual Spreadsheet](http://aosabook.org/images/vistrails/spreadsheet.png)

![그림 23.6: 시각화 스프레드시트](http://aosabook.org/images/vistrails/spreadsheet.png)
