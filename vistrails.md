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
