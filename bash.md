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

### 3.2.3. The Shell Programming Language

### 3.2.3. 셸 프로그래밍 언어

A simple shell command, one with which most readers are most familiar, consists of a command name, such as echo or cd, and a list of zero or more arguments and redirections. Redirections allow the shell user to control the input to and output from invoked commands. As noted above, users can define variables local to simple commands.

대부분의 독자가 알만한 간단한 셸 명령은, echo 나 ed와 같은 명령 이름, 그리고 0개 이상의 파라미터와 리다이렉션으로 이루어져 있습니다. 리다이렉션은 명령으로 주어지는 입력과 명령의 출력을 셸 사용자가 제어할 수 있게 합니다. 위에서 언급했던 것처럼, 사용자들은 이러한 간단한 명령에 지역 변수를 설정할 수 있습니다. 

Reserved words introduce more complex shell commands. There are constructs common to any high-level programming language, such as if-then-else, while, a for loop that iterates over a list of values, and a C-like arithmetic for loop. These more complex commands allow the shell to execute a command or otherwise test a condition and perform different operations based on the result, or execute commands multiple times.

예약어는 조금 더 복잡한 셸 명령을 도입합니다. 여느 다른 고수준 프로그래밍 언어처럼 if-then-else, while, 값의 목록을 탐색하는 for loop, 그리고 C와 유사한 for loop 연산자 등의 구문이 있습니다. 이러한 조금 더 복잡한 명령들은 셸이 명령을 실행하거나, 조건의 만족 여부를 확인하여 그 결과에 따라 다른 작업을 하거나, 명령을 여러 번 실행할 수 있게 합니다. 

One of the gifts Unix brought the computing world is the pipeline: a linear list of commands, in which the output of one command in the list becomes the input of the next. Any shell construct can be used in a pipeline, and it's not uncommon to see pipelines in which a command feeds data to a loop.

유닉스가 컴퓨팅 세계에 가져온 선물은 파이프라인입니다. 파이프라인은, 목록 내의 한 명령의 출력이 그다음 명령의 입력이 되는 명령의 선형 목록입니다. 모든 셸 구문은 파이프라인에서 사용될 수 있으며, 명령이 반복문에 데이터를 제공하는 것은 흔히 볼 수 있는 일입니다.

Bash implements a facility that allows the standard input, standard output, and standard error streams for a command to be redirected to another file or process when the command is invoked. Shell programmers can also use redirection to open and close files in the current shell environment.

Bash는 어떤 명령의 표준 입력, 출력, 그리고 표준 에러 스트림을, 명령이 실행되었을 때 다른 파일이나 프로세스로 리다이렉트 시킬 수 있는 기능을 갖추고 있습니다. 또한, 셸 프로그래머들은 리다이렉션을 이용하여 현재 셸 환경에서 파일을 열거나 닫을 수 있습니다.  

Bash allows shell programs to be stored and used more than once. Shell functions and shell scripts are both ways to name a group of commands and execute the group, just like executing any other command. Shell functions are declared using a special syntax and stored and executed in the same shell's context; shell scripts are created by putting commands into a file and executing a new instance of the shell to interpret them. Shell functions share most of the execution context with the shell that calls them, but shell scripts, since they are interpreted by a new shell invocation, share only what is passed between processes in the environment.

Bash는 셸 프로그램이 저장되어 여러 번 사용할 수 있게 합니다. 셸 함수와 셸 스크립트는 모두 명령의 집합에 이름을 주고 다른 여느 명령처럼 실행하는 방법입니다. 셸 함수들은 같은 셸의 문맥에서 특별한 구문을 이용해 정의, 저장, 그리고 실행됩니다. 셸 스크립트들은 파일 내에 명령을 쓰고, 그 파일을 해석할 새로운 셸 인스턴스를 실행킴으로서 생성됩니다. 셸 함수들은 대부분의 실행 문맥을 자신을 호출한 셸과 공유하지만, 셸 스크립트들은 새로운 셸을 호출하여 해석되기 때문에 환경 간 프로세스끼리 전달된 것들만 공유합니다.

### 3.2.4. A Further Note

### 3.2.4. 읽으면서

As you read further, keep in mind that the shell implements its features using only a few data structures: arrays, trees, singly-linked and doubly-linked lists, and hash tables. Nearly all of the shell constructs are implemented using these primitives.

앞으로 이 장을 읽어 나가는 동안, 셸의 기능은 몇가지 배열, 트리, 연결 리스트, 그리고 해시 테이블 등 몇가지 자료구조만을 사용하여 구현된다는 사실을 염두해 주시길 바랍니다. 거의 모든 셸의 구문들은 이러한 기본형들로 구현되어 있습니다.

The basic data structure the shell uses to pass information from one stage to the next, and to operate on data units within each processing stage, is the WORD_DESC:

셸이 정보를 스테이지간 옮기고, 각 스테이지에서 데이터 단위를 다루는 데 사용하는데 WORD_DESC 라는 자료 구조를 사용합니다. 

	typedef struct word_desc {
	  char *word;           /* Zero terminated string. */
	  int flags;            /* Flags associated with this word. */
	} WORD_DESC;

	typedef struct word_desc {
	  char *word;           /* 널 종료 문자열. */
	  int flags;            /* 이 단어와 연관된 플래그들. */
	} WORD_DESC;

Words are combined into, for example, argument lists, using simple linked lists:

파라미터 목록과 같은 단어들은 간단한 연결 리스트로 합쳐집니다:

	typedef struct word_list {
	  struct word_list *next;
	  WORD_DESC *word;
	} WORD_LIST;

	typedef struct word_list {
	  struct word_list *next;
	  WORD_DESC *word;
	} WORD_LIST;

WORD_LISTs are pervasive throughout the shell. A simple command is a word list, the result of expansion is a word list, and the built-in commands each take a word list of arguments.

WORD_LIST는 셸 어디에서나 찾아볼 수 있을 정도로 흔합니다. 간단한 명령도 word list이며, 확장의 결과도 word list이며, 내장 명령어들도 각각 word list의 파라미터들을 받습니다.

## 3.3. Input Processing

## 3.3. 입력 처리

The first stage of the bash processing pipeline is input processing: taking characters from the terminal or a file, breaking them into lines, and passing the lines to the shell parser to transform into commands. As you would expect, the lines are sequences of characters terminated by newlines.

Bash 처리 파이프라인의 첫 번째 단계는 파일이나 터미널로부터 문자열을 가져와, 줄 단위로 분리하고, 명령으로 변환시키기 위해 셸 파서에 넘겨주는 입력 처리입니다. 예상하셨듯이, 이 줄들은 개행 문자로 끝나는 문자열들의 서열입니다.

### 3.3.1. Readline and Command Line Editing

### 3.3.1. Readline과 커맨드 라인 편집

Bash reads input from the terminal when interactive, and from the script file specified as an argument otherwise. When interactive, bash allows the user to edit command lines as they are typed in, using familiar key sequences and editing commands similar to the Unix emacs and vi editors.

Bash는 대화식으로 작동할 때엔 터미널로부터 입력을 받고, 그 외의 경우엔 파라미터로 지정된 스크립트 파일로부터 입력을 받습니다. 대화식으로 작동할 때 bash는 사용자에게 익숙한 유닉스 emacs나 vi 편집기와 비슷한 입력 서열과 편집 명령을 사용하여 커맨드 라인을 조작할 수 있게 합니다.

Bash uses the readline library to implement command line editing. This provides a set of functions allowing users to edit command lines, functions to save command lines as they are entered, to recall previous commands, and to perform csh-like history expansion. Bash is readline's primary client, and they are developed together, but there is no bash-specific code in readline. Many other projects have adopted readline to provide a terminal-based line editing interface.

Bash는 커맨드 라인 편집을 구현하기 위해 readline 라이브러리를 사용합니다. Readline은 사용자들이 커맨드 라인을 편집하고, 명령이 입력되는 것을 저장하고, 이전 커맨드를 불러오고, csh와 유사한 방식의 히스토리 확장을 하기 위한 함수들을 제공합니다. Bash는 readline의 주 사용자이며, 함께 개발되지만, readline에 bash에 특정한 코드는 없습니다. 수많은 다른 프로젝트들도 터미널 기반 편집 인터페이스를 구현하기 위해 readline을 사용합니다.

Readline also allows users to bind key sequences of unlimited length to any of a large number of readline commands. Readline has commands to move the cursor around the line, insert and remove text, retrieve previous lines, and complete partially-typed words. On top of this, users may define macros, which are strings of characters that are inserted into the line in response to a key sequence, using the same syntax as key bindings. Macros afford readline users a simple string substitution and shorthand facility.

Readline은 사용자들이 입력 서열을 길이 제한 없이 수많은 readline 명령에 바인딩 할 수 있게 해주기도 합니다. 줄 위에서 커서를 옮기고, 문자를 입력하고 삭제하고, 이전 줄을 가져오고, 일부만 입력된 단어를 완성할 수 있는 명령도 제공합니다. 거기에다, 사용자들은 키 바인딩과 같은 구문을 사용해서, 입력 서열에 반응하여 입력되는 문자열인 매크로를 정의할 수도 있습니다. 매크로는 readline 사용자들이 간편한 문자열 치환 및 약칭을 정의할 수 있게 도와줍니다.

#### Readline Structure

#### Readline의 구조

Readline is structured as a basic read/dispatch/execute/redisplay loop. It reads characters from the keyboard using read or equivalent, or obtains input from a macro. Each character is used as an index into a keymap, or dispatch table. Though indexed by a single eight-bit character, the contents of each element of the keymap can be several things. The characters can resolve to additional keymaps, which is how multiple-character key sequences are possible. Resolving to a readline command, such as beginning-of-line, causes that command to be executed. A character bound to the self-insert command is stored into the editing buffer. It's also possible to bind a key sequence to a command while simultaneously binding subsequences to different commands (a relatively recently-added feature); there is a special index into a keymap to indicate that this is done. Binding a key sequence to a macro provides a great deal of flexibility, from inserting arbitrary strings into a command line to creating keyboard shortcuts for complex editing sequences. Readline stores each character bound to self-insert in the editing buffer, which when displayed may occupy one or more lines on the screen.

Readline은 간단한 읽기, 발송, 실행, 재표현의 반복 구조로 되어 있습니다. Readline은 read나, 같은 기능의 함수를 사용하여 키보드로부터 문자열을 읽거나 매크로로부터의 입력을 받습니다. 문자열 하나하나는 키맵이나 발송 테이블의 인덱스로 사용됩니다. 키맵은 하나의 8bit 문자열을 인덱스로 가지지만, 키맵의 각 원소는 여러 가지가 될 수도 있습니다. 문자열들은 추가적인 키맵을 참조할 수 있으며, 이것이 서열이 가능한 이유입니다. 

Readline manages only character buffers and strings using C chars, and builds multibyte characters out of them if necessary. It does not use wchar_t internally for both speed and storage reasons, and because the editing code existed before multibyte character support became widespread. When in a locale that supports multibyte characters, readline automatically reads an entire multibyte character and inserts it into the editing buffer. It's possible to bind multibyte characters to editing commands, but one has to bind such a character as a key sequence; this is possible, but difficult and usually not wanted. The existing emacs and vi command sets do not use multibyte characters, for instance.

Readline은 C char 버퍼와 문자열만 다루고, 필요할 시 같은 타입을 사용하여 멀티바이트 문자열을 만듭니다. 성능과 저장 문제, 그리고 멀티바이트 문자열 지원이 널리 퍼지기 전에 편집 기능을 구현하는 코드가 있었기 때문에 내부적으로 wchar_t를 사용하지 않습니다. Readline은 멀티바이트 문자열을 지원하는 로케일에서는 자동으로 멀티바이트 문자열을 그대로 편집 버퍼에 삽입합니다. 멀티바이트 문자열을 편집 명령에 바인딩할 수는 있지만, 입력 서열로서 바인딩 해야 하며, 어렵고, 주로 원하는 결과를 가져오지 않습니다. 예를 들어, emacs와 vi 명령 집합에서도 멀티바이트 문자열은 사용하지 않습니다.

Once a key sequence finally resolves to an editing command, readline updates the terminal display to reflect the results. This happens regardless of whether the command results in characters being inserted into the buffer, the editing position being moved, or the line being partially or completely replaced. Some bindable editing commands, such as those that modify the history file, do not cause any change to the contents of the editing buffer.

입력 서열이 마침내 편집 명령으로 해석되면, readline은 결과를 반영하도록 터미널 화면을 새로 고칩니다. 이 작업은 편집 명령이 문자열들을 버퍼에 삽입하거나, 편집 위치를 바꾸거나, 명령줄을 부분적이거나 전체적으로 바꾸는 것과 관계없이 실행됩니다.

Updating the terminal display, while seemingly simple, is quite involved. Readline has to keep track of three things: the current contents of the buffer of characters displayed on the screen, the updated contents of that display buffer, and the actual characters displayed. In the presence of multibyte characters, the characters displayed do not exactly match the buffer, and the redisplay engine must take that into account. When redisplaying, readline must compare the current display buffer's contents with the updated buffer, figure out the differences, and decide how to most efficiently modify the display to reflect the updated buffer. This problem has been the subject of considerable research through the years (the string-to-string correction problem). Readline's approach is to identify the beginning and end of the portion of the buffer that differs, compute the cost of updating just that portion, including moving the cursor backward and forward (e.g., will it take more effort to issue terminal commands to delete characters and then insert new ones than to simply overwrite the current screen contents?), perform the lowest-cost update, then clean up by removing any characters remaining at the end of the line if necessary and position the cursor in the correct spot.

터미널 화면을 새로 고치는 일은 단순해 보이지만, 사실은 꽤 복잡한 작업입니다. Readline은 지금 화면에 표시된 문자열들의 버퍼, 업데이트된 해당 버퍼의 내용, 그리고 실제로 화면에 표시되는 문자열들의, 세 가지의 상태를 따라가야 합니다. 멀티바이트 문자열이 존재하는 경우 화면 갱신 엔진은 화면에 표시된 문자열들은 버퍼와 완벽히 일치하지 않는다는 점을 고려해야 합니다. 화면을 새로 고칠 때 readline은 현재 화면 버퍼의 내용과 업데이트된 버퍼의 차이점을 비교하여, 화면이 업데이트된 버퍼를 반영할 수 있는 가장 효율적인 편집 방법을 계산해야 합니다. 이 문제는 수년간 상당한 수의 연구 주제(string-to-string correction 문제)로 다루어졌습니다. 이 문제에 대해 readline은, 버퍼 간 차이가 발생하는 영역의 처음과 끝을 확인하고, 커서를 앞뒤로 옮기는 비용을 고려하여(문자열들을 삭제하는 명령을 호출하고 새로 쓰는 것과 화면의 내용을 덮어쓰는 것 중 어느 쪽이 더 싸게 먹힐까?) 해당 영역만을 갱신하는 비용을 계산하고, 최저 비용으로 화면을 갱신한 후, 필요한 경우 줄 끝에 남은 문자열들을 삭제하고 커서를 올바른 위치로 옮겨 마무리하는, 접근 방식을 취합니다.

The redisplay engine is without question the one piece of readline that has been modified most heavily. Most of the changes have been to add functionality—most significantly, the ability to have non-displaying characters in the prompt (to change colors, for instance) and to cope with characters that take up more than a single byte.

화면 갱신 엔진은 readline의 구성 요소 중 가장 자주 편집되는 부분 중 하나일 것입니다. 대부분의 변경점은 기능을 추가하기 위함이며, 특히 표시되지 않는 문자열들을 명령줄에 포함하는 기능(예를 들어, 색을 바꾸는 기능)과 멀티바이트 문자열을 처리하기 위한 기능이 상당수를 차지합니다.

Readline returns the contents of the editing buffer to the calling application, which is then responsible for saving the possibly-modified results in the history list.

Readline은 편집 버퍼를 자신을 호출한 프로그램에 전달하며, 변경되었을 수도 있는 버퍼를 히스토리 목록에 저장하는 것은 해당 프로그램의 몫입니다.
