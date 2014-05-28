# 3. The Bourne-Again Shell

# 3. Bourne-Again Shell

## 3.1. Introduction

## 3.1. 서론

A Unix shell provides an interface that lets the user interact with the operating system by running commands. But a shell is also a fairly rich programming language: there are constructs for flow control, alternation, looping, conditionals, basic mathematical operations, named functions, string variables, and two-way communication between the shell and the commands it invokes.

유닉스 셸은 명령을 실행하는 방식으로 사용자들에게 운영체제와 상호 작용하기 위한 인터페이스를 제공합니다. 하지만 셸은 꽤 풍부한 프로그래밍 언어이기도 합니다. 그 예시로, 셸은 흐름 제어, 반복문, 조건문, 기본적인 연산, 기명 함수, 문자열 변수, 그리고 셸과 실행되는 명령 간의 통신을 위한 구문을 제공합니다.

Shells can be used interactively, from a terminal or terminal emulator such as xterm, and non-interactively, reading commands from a file. Most modern shells, including bash, provide command-line editing, in which the command line can be manipulated using emacs- or vi-like commands while it's being entered, and various forms of a saved history of commands.

셸은 xterm 등의 터미널 에뮬레이터를 통해 대화식으로 사용하거나, 파일을 통해 명령을 전달하는 비대화식으로도 사용할 수 있습니다. bash를 포함하여 대부분의 현대적인 셸은 커맨드 라인을 emacs나 vi의 키 바인딩을 통해 편집할 수 있으며, 여러 형태로 과거에 실행하였던 명령들을 저장하여 제공합니다.

Bash processing is much like a shell pipeline: after being read from the terminal or a script, data is passed through a number of stages, transformed at each step, until the shell finally executes a command and collects its return status.

Bash의 데이터 처리 방식은 셸 파이프라인과 비슷합니다. 데이터는 터미널이나 스크립트를 통해 읽어진 다음, 셸이 명령을 실행하고 리턴값을 받아 오게 될 때까지 몇 단계를 거쳐 변형되는 과정을 거칩니다.

This chapter will explore bash's major components: input processing, parsing, the various word expansions and other command processing, and command execution, from the pipeline perspective. These components act as a pipeline for data read from the keyboard or from a file, turning it into an executed command.

이번 장에서는 파이프라인의 관점에서 bash의 입력 처리, 구문 분석, 단어 단위 확장, 그리고 명령 실행까지의 구성 요소를 파악할 것입니다. 이러한 구성 요소들은 키보드나 파일로부터 읽은 데이터를 실행 가능한 명령으로 바꾸기 위한 파이프라인의 역할을 합니다.

### 3.1.1. Bash

### 3.1.1. Bash

Bash is the shell that appears in the GNU operating system, commonly implemented atop the Linux kernel, and several other common operating systems, most notably Mac OS X. It offers functional improvements over historical versions of sh for both interactive and programming use.

Bash는 리눅스 커널 기반으로 구현된 GNU 운영체제와 몇몇 다른 일반적인 운영체제, 특히 OS X에 탑재된 셸입니다. Bash는 대화식 사용은 물론 프로그래밍 용도로도 sh와 비교되는 개선사항을 제공합니다.

The name is an acronym for Bourne-Again SHell, a pun combining the name of Stephen Bourne (the author of the direct ancestor of the current Unix shell /bin/sh, which appeared in the Bell Labs Seventh Edition Research version of Unix) with the notion of rebirth through reimplementation. The original author of bash was Brian Fox, an employee of the Free Software Foundation. I am the current developer and maintainer, a volunteer who works at Case Western Reserve University in Cleveland, Ohio.

Bash의 이름은 스티븐 본(현 유닉스 셸인 /bin/sh의, Bell Labs 유닉스 7판의 연구용 버전에서 처음 등장한, 직속 조상 프로그램의 개발자이다)의 이름과 재구현을 통한 재탄생의 개념을 합친 말장난인 Bourne-Again SHell의 두문자어입니다. bash의 원저작자는 자유 소프트웨어 재단의 직원인 브라이언 폭스이며, 지금은 오하이오 클리브랜드에 있는 베이스 웨스턴 리저브 대학에서 자원봉사를 하고 있는 제가 개발과 유지를 맡고 있습니다.

Like other GNU software, bash is quite portable. It currently runs on nearly every version of Unix and a few other operating systems—independently-supported ports exist for hosted Windows environments such as Cygwin and MinGW, and ports to Unix-like systems such as QNX and Minix are part of the distribution. It only requires a Posix environment to build and run, such as one provided by Microsoft's Services for Unix (SFU).

다른 GNU 소프트웨어처럼, bash는 꽤 포터블합니다. 현재 거의 모든 버전의 유닉스에서 작동하며, Cygwin이나 MinGW처럼 Windows 호스트 환경에서 자체적으로 이식한 버전이 존재하며, QNX와 Minix 같은 Unix-like 운영체제를 위해 이식된 버전도 함께 배포합니다. Microsoft's Services for Unix(SFU)에서 제공하는 환경처럼 Posix 환경만 있으면 빌드 및 실행할 수 있습니다.

## 3.2. Syntactic Units and Primitives

## 3.2. 구문 단위와 기본형

### 3.2.1. Primitives

### 3.2.1. 기본형

To bash, there are basically three kinds of tokens: reserved words, words, and operators. Reserved words are those that have meaning to the shell and its programming language; usually these words introduce flow control constructs, like if and while. Operators are composed of one or more metacharacters: characters that have special meaning to the shell on their own, such as | and >. The rest of the shell's input consists of ordinary words, some of which have special meaning—assignment statements or numbers, for instance—depending on where they appear on the command line.

Bash에는 예약어, 단어, 연산자의 세 종류의 토큰이 있습니다. 예약어는 if나 while 등의 흐름 제어 구문을 제공하기 위한 셸과 셸의 프로그래밍 언어에서 의미를 지니는 단어들입니다. 연산자들은 |와 > , 셸에서 독립적으로 의미를 가지는 문자들이며, 하나 이상의 메타 문자로 이루어져 있습니다. 셸의 나머지 입력은 보통의 단어들로 이루어져 있으며, 그중 몇몇 단어들은 커맨드 라인에서 나타나는 위치에 따라 의미를 가지는 등, 특별한 의미를 부여하는 대입문이나 숫자들입니다.

### 3.2.2. Variables and Parameters

### 3.2.2. 변수와 파라미터

As in any programming language, shells provide variables: names to refer to stored data and operate on it. The shell provides basic user-settable variables and some built-in variables referred to as parameters. Shell parameters generally reflect some aspect of the shell's internal state, and are set automatically or as a side effect of another operation.

다른 프로그래밍 언어들과 마찬가지로, 셸도 저장된 자료를 가리키고 관리하기 위한 변수를 제공합니다. 셸은 사용자가 설정 가능한 기본적인 변수와 파라미터라고 불리는 내장 변수를 제공합니다. 셸 파라미터는 대부분의 경우 셸의 내부 상태 일부를 반영하며, 자동으로 설정되거나 다른 작업의 작용으로 설정됩니다.

Variable values are strings. Some values are treated specially depending on context; these will be explained later. Variables are assigned using statements of the form name=value. The value is optional; omitting it assigns the empty string to name. If the value is supplied, the shell expands the value and assigns it to name. The shell can perform different operations based on whether or not a variable is set, but assigning a value is the only way to set a variable. Variables that have not been assigned a value, even if they have been declared and given attributes, are referred to as unset.

변수들의 값은 문자열입니다. 몇몇 변수들은 문맥에 따라 특별하게 다뤄지는데, 이러한 값들에 대해서는 나중에 다뤄집니다. 변수들은 이름=값의 형태로 지정됩니다. 이 값은 선택적이며, 생략할 경우 이름에 빈 문자열이 지정됩니다. 값이 지정된 경우 셸은 값을 확장한 후에 확장된 값을 이름에 지정합니다. 셸은 변수의 설정 여부에 따라 다른 작업을 할 수 있지만, 변수를 설정하기 위해서는 값을 지정하는 방법이 유일합니다. 값이 지정되지 않은 변수들은 속성이 선언되어 지정되어도 설정되지 않았다고 합니다.

A word beginning with a dollar sign introduces a variable or parameter reference. The word, including the dollar sign, is replaced with the value of the named variable. The shell provides a rich set of expansion operators, from simple value replacement to changing or removing portions of a variable's value that match a pattern.

달러 기호로 시작하는 단어는 변수 또는 파라미터 참조를 도입합니다. 달러 기호를 포함하여, 그 단어는 기명 변수의 값으로 교체됩니다. 셸은 단순한 값 치환부터, 변숫값의 형식에 따라 변수의 일부를 바꾸거나 변형시킬 수도 있는 풍부한 확장 연산자를 제공합니다.

There are provisions for local and global variables. By default, all variables are global. Any simple command (the most familiar type of command—a command name and optional set of arguments and redirections) may be prefixed by a set of assignment statements to cause those variables to exist only for that command. The shell implements stored procedures, or shell functions, which can have function-local variables.

전역 변수와 지역 변수를 규정하는 방법들이 있습니다. 기본적으로 모든 변수는 전역 변수입니다. 어떠한 단순한 명령(익숙한 명령 종류를 예로 들자면, 명령 이름과 선택적인 파라미터와 리다이렉션)도 대입문의 접두어를 붙여 해당 명령 안의 변수들을 그 명령 안에서만 존재하도록 할 수 있습니다. 셸은 함수에 대해 지역적인 변수를 가질 수 있는 저장된 프로지셔, 즉 셸 함수를 구현합니다.

Variables can be minimally typed: in addition to simple string-valued variables, there are integers and arrays. Integer-typed variables are treated as numbers: any string assigned to them is expanded as an arithmetic expression and the result is assigned as the variable's value. Arrays may be indexed or associative; indexed arrays use numbers as subscripts, while associative arrays use arbitrary strings. Array elements are strings, which can be treated as integers if desired. Array elements may not be other arrays.

변수는 최소한으로 타이핑될 수 있습니다. 문자열 값을 가진 단순한 변수 외에도, 정수와 배열을 지정할 수 있습니다. 정수 타입의 변수들은 숫자로 취급됩니다. 이러한 변수에 문자열이 지정될 땐 수식으로 확장되어, 그 결과가 변수의 값으로 지정됩니다. 배열은 인덱스를 사용할 수도 있고 연관 관계를 사용할 수도 있습니다. 인덱스 배열은 숫자를, 연관 배열은 문자열을 첨자로 사용합니다. 배열의 원소는 문자열이며, 필요한 경우 정수로 취급할 수도 있습니다. 배열의 원소는 또 다른 배열이 될 수 없습니다.

Bash uses hash tables to store and retrieve shell variables, and linked lists of these hash tables to implement variable scoping. There are different variable scopes for shell function calls and temporary scopes for variables set by assignment statements preceding a command. When those assignment statements precede a command that is built into the shell, for instance, the shell has to keep track of the correct order in which to resolve variable references, and the linked scopes allow bash to do that. There can be a surprising number of scopes to traverse depending on the execution nesting level.

Bash는 셸 변수를 저장하기 위해 해시 테이블을, 변수 영역을 구분하기 위해 이 해시 테이블들의 연결 리스트를 사용합니다. 셸 함수 호출들을 위한 각각의 변수 영역과, 명령 이전에 오는 대입문들을 위한 임시 변수 영역들이 있습니다. 예를 들어 이러한 대입문들이 셸에 내장된 명령 이전에 오는 경우 셸은 변수 참조를 분석하는 올바른 순서를 기억하고 있어야 하며, 이때 변수 영역의 연결 리스트를 사용하게 됩니다. 실행 깊이에 따라 놀라울 정도로 많은 수의 변수 영역을 탐색해야 할 수도 있습니다.
