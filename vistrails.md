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
