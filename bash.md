# 3. Bourne-Again Shell

## 3.1. 서론

유닉스 셸은 사용자가 운영체제와 상호 작용하기 위한 명령 실행 인터페이스를 제공합니다. 하지만 셸은 풍부한 프로그래밍 언어이기도 합니다. 셸은 흐름 제어, 반복문, 조건문, 기본적인 연산, 기명 함수, 문자열 변수를 위한 구문과, 셸과 셸이 실행한 명령 간의 쌍방향 통신을 위한 구조를 제공합니다.

셸은 xterm 같은 터미널 에뮬레이터를 통해 대화식으로 사용하거나, 파일을 통해 명령을 읽는 비대화식으로 사용할 수 있습니다. Bash를 포함한 대부분의 현대적인 셸은 커맨드 라인을 입력하는 동시에 emacs나 vi의 키 바인딩을 사용해서 편집할 수 있으며, 실행하였던 명령들의 기록을 저장하여 다양한 형태로 제공합니다.

Bash의 데이터 처리 방식은 셸 파이프라인과 비슷합니다. 데이터는 터미널이나 스크립트를 통해 읽힌 후, 셸이 명령을 실행하고 반환값을 받아 오게 될 때까지, 여러 단계의 변형 과정을 거칩니다.

이번 장에서는 bash의 입력 처리, 구문 분석, 단어 확장, 그리고 명령 실행까지의 구성 요소를 파이프라인의 관점에서 살펴볼 것입니다. 이러한 구성 요소들은 키보드나 파일로부터 데이터를 읽어 명령을 실행하기 위한 파이프라인의 역할을 합니다.

![Bash 구성 요소의 설계](http://aosabook.org/images/bash/bash-article-diagram.png)

### 3.1.1. Bash

### 3.1.1. Bash

Bash is the shell that appears in the GNU operating system, commonly implemented atop the Linux kernel, and several other common operating systems, most notably Mac OS X. It offers functional improvements over historical versions of sh for both interactive and programming use.

Bash는 리눅스 커널 기반으로 구현된 GNU 운영체제와 몇몇 다른 일반적인 운영체제, 특히 OS X에 탑재된 셸입니다. Bash는 대화식 사용은 물론 프로그래밍 용도로도 sh와 비교되는 개선사항을 제공합니다.

The name is an acronym for Bourne-Again SHell, a pun combining the name of Stephen Bourne (the author of the direct ancestor of the current Unix shell `/bin/sh`, which appeared in the Bell Labs Seventh Edition Research version of Unix) with the notion of rebirth through reimplementation. The original author of bash was Brian Fox, an employee of the Free Software Foundation. I am the current developer and maintainer, a volunteer who works at Case Western Reserve University in Cleveland, Ohio.

Bash의 이름은 스티븐 본(현 유닉스 셸인 `/bin/sh`의, Bell Labs 유닉스 7판의 연구용 버전에서 처음 등장한, 직속 조상 프로그램의 개발자이다)의 이름과 재구현을 통한 재탄생의 개념을 합친 말장난인 Bourne-Again SHell의 두문자어입니다. bash의 원저작자는 자유 소프트웨어 재단의 직원인 브라이언 폭스이며, 지금은 오하이오 클리브랜드에 있는 베이스 웨스턴 리저브 대학에서 자원봉사를 하고 있는 제가 개발과 유지를 맡고 있습니다.

Like other GNU software, bash is quite portable. It currently runs on nearly every version of Unix and a few other operating systems—independently-supported ports exist for hosted Windows environments such as Cygwin and MinGW, and ports to Unix-like systems such as QNX and Minix are part of the distribution. It only requires a Posix environment to build and run, such as one provided by Microsoft's Services for Unix (SFU).

다른 GNU 소프트웨어처럼, bash는 꽤 포터블합니다. 현재 거의 모든 버전의 유닉스에서 작동하며, Cygwin이나 MinGW처럼 Windows 호스트 환경에서 자체적으로 이식한 버전이 존재하며, QNX와 Minix 같은 Unix-like 운영체제를 위해 이식된 버전도 함께 배포합니다. Microsoft's Services for Unix(SFU)에서 제공하는 환경처럼 Posix 환경만 있으면 빌드 및 실행할 수 있습니다.

## 3.2. Syntactic Units and Primitives

## 3.2. 구문 단위와 기본형

### 3.2.1. Primitives

### 3.2.1. 기본형

To bash, there are basically three kinds of tokens: reserved words, words, and operators. Reserved words are those that have meaning to the shell and its programming language; usually these words introduce flow control constructs, like `if` and `while`. Operators are composed of one or more metacharacters: characters that have special meaning to the shell on their own, such as `|` and `>`. The rest of the shell's input consists of ordinary words, some of which have special meaning—assignment statements or numbers, for instance—depending on where they appear on the command line.

Bash에는 예약어, 단어, 연산자의 세 종류의 토큰이 있습니다. 예약어는 `if`나 `while` 등의 흐름 제어 구문을 제공하기 위한 셸과 셸의 프로그래밍 언어에서 의미를 지니는 단어들입니다. 연산자들은 `|`와 `>` , 셸에서 독립적으로 의미를 가지는 문자들이며, 하나 이상의 메타 문자로 이루어져 있습니다. 셸의 나머지 입력은 보통의 단어들로 이루어져 있으며, 그중 몇몇 단어들은 커맨드 라인에서 나타나는 위치에 따라 의미를 가지는 등, 특별한 의미를 부여하는 대입문이나 숫자들입니다.

### 3.2.2. Variables and Parameters

### 3.2.2. 변수와 파라미터

As in any programming language, shells provide variables: names to refer to stored data and operate on it. The shell provides basic user-settable variables and some built-in variables referred to as parameters. Shell parameters generally reflect some aspect of the shell's internal state, and are set automatically or as a side effect of another operation.

다른 프로그래밍 언어들과 마찬가지로, 셸도 저장된 자료를 가리키고 관리하기 위한 변수를 제공합니다. 셸은 사용자가 설정 가능한 기본적인 변수와 파라미터라고 불리는 내장 변수를 제공합니다. 셸 파라미터는 대부분의 경우 셸의 내부 상태 일부를 반영하며, 자동으로 설정되거나 다른 작업의 작용으로 설정됩니다.

Variable values are strings. Some values are treated specially depending on context; these will be explained later. Variables are assigned using statements of the form `name=value`. The `value` is optional; omitting it assigns the empty string to `name`. If the value is supplied, the shell expands the value and assigns it to `name`. The shell can perform different operations based on whether or not a variable is set, but assigning a value is the only way to set a variable. Variables that have not been assigned a value, even if they have been declared and given attributes, are referred to as unset.

변수들의 값은 문자열입니다. 몇몇 변수들은 문맥에 따라 특별하게 다뤄지는데, 이러한 값들에 대해서는 나중에 다뤄집니다. 변수들은 `name=value`의 형태로 지정됩니다. `value`는 선택적이며, 생략할 경우 `name`에 빈 문자열이 지정됩니다. 값이 지정된 경우 셸은 값을 확장한 후에 확장된 값을 `name`에 지정합니다. 셸은 변수의 설정 여부에 따라 다른 작업을 할 수 있지만, 변수를 설정하기 위해서는 값을 지정하는 방법이 유일합니다. 값이 지정되지 않은 변수들은 속성이 선언되어 지정되어도 설정되지 않았다고 합니다.

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

A simple shell command, one with which most readers are most familiar, consists of a command name, such as `echo` or `cd`, and a list of zero or more arguments and redirections. Redirections allow the shell user to control the input to and output from invoked commands. As noted above, users can define variables local to simple commands.

대부분의 독자가 알만한 간단한 셸 명령은, `echo` 나 `ed`와 같은 명령 이름, 그리고 0개 이상의 파라미터와 리다이렉션으로 이루어져 있습니다. 리다이렉션은 명령으로 주어지는 입력과 명령의 출력을 셸 사용자가 제어할 수 있게 합니다. 위에서 언급했던 것처럼, 사용자들은 이러한 간단한 명령에 지역 변수를 설정할 수 있습니다. 

Reserved words introduce more complex shell commands. There are constructs common to any high-level programming language, such as `if-then-else`, `while`, a `for` loop that iterates over a list of values, and a C-like arithmetic for loop. These more complex commands allow the shell to execute a command or otherwise test a condition and perform different operations based on the result, or execute commands multiple times.

예약어는 조금 더 복잡한 셸 명령을 도입합니다. 여느 다른 고수준 프로그래밍 언어처럼 `if-then-else`, `while`, 값의 목록을 탐색하는 `for` 반복문, 그리고 C와 유사한 for loop 연산자 등의 구문이 있습니다. 이러한 조금 더 복잡한 명령들은 셸이 명령을 실행하거나, 조건의 만족 여부를 확인하여 그 결과에 따라 다른 작업을 하거나, 명령을 여러 번 실행할 수 있게 합니다. 

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

The basic data structure the shell uses to pass information from one stage to the next, and to operate on data units within each processing stage, is the `WORD_DESC`:

셸이 정보를 스테이지간 옮기고, 각 스테이지에서 데이터 단위를 다루는 데 사용하는데 `WORD_DESC` 이라는 자료 구조를 사용합니다. 

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

`WORD_LIST`s are pervasive throughout the shell. A simple command is a word list, the result of expansion is a word list, and the built-in commands each take a word list of arguments.

`WORD_LIST`는 셸 어디에서나 찾아볼 수 있을 정도로 많이 사용됩니다. 간단한 명령도 word list이며, 확장의 결과도 word list이며, 내장 명령어들도 각각 word list의 파라미터들을 받습니다.

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

Readline is structured as a basic read/dispatch/execute/redisplay loop. It reads characters from the keyboard using `read` or equivalent, or obtains input from a macro. Each character is used as an index into a keymap, or dispatch table. Though indexed by a single eight-bit character, the contents of each element of the keymap can be several things. The characters can resolve to additional keymaps, which is how multiple-character key sequences are possible. Resolving to a readline command, such as `beginning-of-line`, causes that command to be executed. A character bound to the `self-insert` command is stored into the editing buffer. It's also possible to bind a key sequence to a command while simultaneously binding subsequences to different commands (a relatively recently-added feature); there is a special index into a keymap to indicate that this is done. Binding a key sequence to a macro provides a great deal of flexibility, from inserting arbitrary strings into a command line to creating keyboard shortcuts for complex editing sequences. Readline stores each character bound to `self-insert` in the editing buffer, which when displayed may occupy one or more lines on the screen.

Readline은 간단한 읽기, 발송, 실행, 재표현의 반복 구조로 되어 있습니다. Readline은 `read`나, 같은 기능의 함수를 사용하여 키보드로부터 문자열을 읽거나 매크로로부터의 입력을 받습니다. 문자열 하나하나는 키맵이나 발송 테이블의 인덱스로 사용됩니다. 키맵은 하나의 8bit 문자열을 인덱스로 가지지만, 키맵의 각 원소는 여러 가지가 될 수도 있습니다. 문자열들은 추가적인 키맵을 참조할 수 있으며, 이것이 서열이 가능한 이유입니다. 

Readline manages only character buffers and strings using C `char`s, and builds multibyte characters out of them if necessary. It does not use `wchar_t` internally for both speed and storage reasons, and because the editing code existed before multibyte character support became widespread. When in a locale that supports multibyte characters, readline automatically reads an entire multibyte character and inserts it into the editing buffer. It's possible to bind multibyte characters to editing commands, but one has to bind such a character as a key sequence; this is possible, but difficult and usually not wanted. The existing emacs and vi command sets do not use multibyte characters, for instance.

Readline은 C `char` 버퍼와 문자열만 다루고, 필요할 시 같은 타입을 사용하여 멀티바이트 문자열을 만듭니다. 성능과 저장 문제, 그리고 멀티바이트 문자열 지원이 널리 퍼지기 전에 편집 기능을 구현하는 코드가 있었기 때문에 내부적으로 `wchar_t`를 사용하지 않습니다. Readline은 멀티바이트 문자열을 지원하는 로케일에서는 자동으로 멀티바이트 문자열을 그대로 편집 버퍼에 삽입합니다. 멀티바이트 문자열을 편집 명령에 바인딩할 수는 있지만, 입력 서열로서 바인딩 해야 하며, 어렵고, 주로 원하는 결과를 가져오지 않습니다. 예를 들어, emacs와 vi 명령 집합에서도 멀티바이트 문자열은 사용하지 않습니다.

Once a key sequence finally resolves to an editing command, readline updates the terminal display to reflect the results. This happens regardless of whether the command results in characters being inserted into the buffer, the editing position being moved, or the line being partially or completely replaced. Some bindable editing commands, such as those that modify the history file, do not cause any change to the contents of the editing buffer.

입력 서열이 마침내 편집 명령으로 해석되면, readline은 결과를 반영하도록 터미널 화면을 새로 고칩니다. 이 작업은 편집 명령이 문자열들을 버퍼에 삽입하거나, 편집 위치를 바꾸거나, 명령줄을 부분적이거나 전체적으로 바꾸는 것과 관계없이 실행됩니다.

Updating the terminal display, while seemingly simple, is quite involved. Readline has to keep track of three things: the current contents of the buffer of characters displayed on the screen, the updated contents of that display buffer, and the actual characters displayed. In the presence of multibyte characters, the characters displayed do not exactly match the buffer, and the redisplay engine must take that into account. When redisplaying, readline must compare the current display buffer's contents with the updated buffer, figure out the differences, and decide how to most efficiently modify the display to reflect the updated buffer. This problem has been the subject of considerable research through the years (the string-to-string correction problem). Readline's approach is to identify the beginning and end of the portion of the buffer that differs, compute the cost of updating just that portion, including moving the cursor backward and forward (e.g., will it take more effort to issue terminal commands to delete characters and then insert new ones than to simply overwrite the current screen contents?), perform the lowest-cost update, then clean up by removing any characters remaining at the end of the line if necessary and position the cursor in the correct spot.

터미널 화면을 새로 고치는 일은 단순해 보이지만, 사실은 꽤 복잡한 작업입니다. Readline은 지금 화면에 표시된 문자열들의 버퍼, 업데이트된 해당 버퍼의 내용, 그리고 실제로 화면에 표시되는 문자열들의, 세 가지의 상태를 따라가야 합니다. 멀티바이트 문자열이 존재하는 경우 화면 갱신 엔진은 화면에 표시된 문자열들은 버퍼와 완벽히 일치하지 않는다는 점을 고려해야 합니다. 화면을 새로 고칠 때 readline은 현재 화면 버퍼의 내용과 업데이트된 버퍼의 차이점을 비교하여, 화면이 업데이트된 버퍼를 반영할 수 있는 가장 효율적인 편집 방법을 계산해야 합니다. 이 문제는 수년간 상당한 수의 연구 주제(string-to-string correction 문제)로 다루어졌습니다. 이 문제에 대해 readline은, 버퍼 간 차이가 발생하는 영역의 처음과 끝을 확인하고, 커서를 앞뒤로 옮기는 비용을 고려하여(문자열들을 삭제하는 명령을 호출하고 새로 쓰는 것과 화면의 내용을 덮어쓰는 것 중 어느 쪽이 더 싸게 먹힐까?) 해당 영역만을 갱신하는 비용을 계산하고, 최저 비용으로 화면을 갱신한 후, 필요한 경우 줄 끝에 남은 문자열들을 삭제하고 커서를 올바른 위치로 옮겨 마무리하는, 접근 방식을 취합니다.

The redisplay engine is without question the one piece of readline that has been modified most heavily. Most of the changes have been to add functionality—most significantly, the ability to have non-displaying characters in the prompt (to change colors, for instance) and to cope with characters that take up more than a single byte.

화면 갱신 엔진은 readline의 구성 요소 중 가장 자주 편집되는 부분 중 하나일 것입니다. 대부분의 변경점은 기능을 추가하기 위함이며, 특히 표시되지 않는 문자열들을 명령줄에 포함하는 기능(예를 들어, 색을 바꾸는 기능)과 멀티바이트 문자열을 처리하기 위한 기능이 상당수를 차지합니다.

Readline returns the contents of the editing buffer to the calling application, which is then responsible for saving the possibly-modified results in the history list.

Readline은 편집 버퍼를 자신을 호출한 프로그램에 전달하며, 변경되었을 수도 있는 버퍼를 히스토리 목록에 저장하는 것은 해당 프로그램의 몫입니다.

#### Applications Extending Readline

#### Readline을 확장하는 프로그램

Just as readline offers users a variety of ways to customize and extend readline's default behavior, it provides a number of mechanisms for applications to extend its default feature set. First, bindable readline functions accept a standard set of arguments and return a specified set of results, making it easy for applications to extend readline with application-specific functions. Bash, for instance, adds more than thirty bindable commands, from bash-specific word completions to interfaces to shell built-in commands.

Readline이 사용자들에게 readline의 기본 작동 방식을 커스터마이즈하고 확장할 수 있는 다양한 수단을 제공하는 것처럼, 응용 프로그램들에도 readline의 기본적인 기능 집합을 확장할 수 있는 몇 가지 방법을 제공합니다. 첫 번째로, 바인딩 가능한 readline 함수들은 표준적인 파라미터 집합을 받아 특정한 결과를 전달할 수 있어, 응용 프로그램들이 해당 프로그램에 종속적인 함수로 readline을 확장하기 쉽게 해 줍니다. 예를 들어, Bash는 bash에 종속적인 단어 완성부터, 셸 내장 명령 인터페이스까지, 30가지 이상의 바인딩 가능한 함수를 더합니다.

The second way readline allows applications to modify its behavior is through the pervasive use of pointers to hook functions with well-known names and calling interfaces. Applications can replace some portions of readline's internals, interpose functionality in front of readline, and perform application-specific transformations.

응용 프로그램이 readline의 작동 방식을 변경할 수 있게 해주는 두 번째 방법은, 포인터를 여러 곳에서 사용하여, 함수를 잘 알려진 이름과 호출 인터페이스에 후킹 하는 것입니다. 응용 프로그램들은 readline 내부 일부를 교체하고, readline 앞에 기능을 끼워 넣거나, 응용 프로그램에 종속적인 변형을 가할 수 있습니다.

### 3.3.2. Non-interactive Input Processing

### 3.3.2. 비대화식 입력 처리

When the shell is not using readline, it uses either `stdio` or its own buffered input routines to obtain input. The bash buffered input package is preferable to `stdio` when the shell is not interactive because of the somewhat peculiar restrictions Posix imposes on input consumption: the shell must consume only the input necessary to parse a command and leave the rest for executed programs. This is particularly important when the shell is reading a script from the standard input. The shell is allowed to buffer input as much as it wants, as long as it is able to roll the file offset back to just after the last character the parser consumes. As a practical matter, this means that the shell must read scripts a character at a time when reading from non-seekable devices such as pipes, but may buffer as many characters as it likes when reading from files.

셸이 readline을 사용하지 않을 땐 `stdio`나 셸 자체의 버퍼링된 입력 루틴을 사용하여 입력을 받습니다. 셸이 비대화식으로 동작할 땐, `stdio`에 비해 Bash의 버퍼팅된 입력 패키지가 선호되는데, 셸이 명령을 구문분석하는 데 필요한 입력만 소비하고 나머지는 실행되는 프로그램을 위해 남기게 하는 Posix의 까다로운 제한 때문입니다. 셸이 스크립트를 표준 입력으로부터 받을 때 특히 중요한데, 셸은 구문 분석기가 마지막으로 읽은 문자열 바로 앞으로 파일 오프셋을 되돌릴 수 있는 이상 원하는 만큼 입력을 버퍼링할 수 있습니다. 실용적인 관점에서 볼 때, 이것은 셸이 파이프 등 탐색 불가능한 디바이스로부터 읽을 때엔 스크립트들을 한 번에 문자열 하나씩만을 읽어야 하지만, 파일을 읽을 때엔 원하는 만큼 문자열 버퍼링을 할 수 있다는 의미를 가집니다.

These idiosyncrasies aside, the output of the non-interactive input portion of shell processing is the same as readline: a buffer of characters terminated by a newline.

이런 특성은 제쳐두고, 셸의 비대화식 입력 처리의 출력은, 개행문자로 끝나는 문자열 버퍼라는 점에서 readline과 같습니다.

### 3.3.3. Multibyte Characters

### 3.3.3. 멀티바이트 문자열

Multibyte character processing was added to the shell a long time after its initial implementation, and it was done in a way designed to minimize its impact on the existing code. When in a locale that supports multibyte characters, the shell stores its input in a buffer of bytes (C `char`s), but treats these bytes as potentially multibyte characters. Readline understands how to display multibyte characters (the key is knowing how many screen positions a multibyte character occupies, and how many bytes to consume from a buffer when displaying a character on the screen), how to move forward and backward in the line a character at a time, as opposed to a byte at a time, and so on. Other than that, multibyte characters don't have much effect on shell input processing. Other parts of the shell, described later, need to be aware of multibyte characters and take them into account when processing their input.

멀티바이트 문자열 처리는 셸의 초기 구현이 생긴지 한참 뒤에 기존 코드에 미치는 영향을 최소화시키는 방향으로 추가되었습니다. 멀티바이트 문자열을 지원하는 로케일에서 셸은 입력을 바이트 버퍼(C `char`)에 저장하지만, 이 바이트 열이 멀티바이트 문자열일 수 있다고 가정합니다. Readline은 멀티바이트 문자열을 화면에 표시하는 방법(멀티바이트 문자열이 화면 영역을 얼마나 차지하고 있는지, 문자를 화면에 표시할 때 버퍼에서 읽어야 할 바이트 수를 알고 있는 것이 핵심), 줄 위에서 바이트 단위가 아니라, 한 문자씩 왔다 갔다 하는 방법, 등을 알고 있습니다. 그 외에는, 멀티바이트 문자열은 셸의 입력 처리에 별다른 영향을 미치지 않습니다. 이후에 다뤄질 셸의 다른 부분에서는 멀티바이트 문자열을 인식할 수 있어야 하며, 입력 처리를 할 때 고려해야 합니다.

## 3.4. Parsing

## 3.4. 구문 분석

The initial job of the parsing engine is lexical analysis: to separate the stream of characters into words and apply meaning to the result. The word is the basic unit on which the parser operates. Words are sequences of characters separated by metacharacters, which include simple separators like spaces and tabs, or characters that are special to the shell language, like semicolons and ampersands.

구문 분석 엔진의 첫번째 일은 문자열 스트림을 단어로 나누고 결과에 의미를 부여하는 낱말 분석입니다. 낱말은 구문 분석기가 동작하는 기본적인 단위입니다. 낱말은 메타 문자로 분리된 문자열이며, 메타 문자는 공백이나 탭 등 단순한 구분자나, 세미콜론이나 앰퍼샌드 등 셸에서 특별한 의미를 지니는 문자들을 포함합니다.

One historical problem with the shell, as Tom Duff said in his paper about rc, the Plan 9 shell, is that nobody really knows what the Bourne shell grammar is. The Posix shell committee deserves significant credit for finally publishing a definitive grammar for a Unix shell, albeit one that has plenty of context dependencies. That grammar isn't without its problems—it disallows some constructs that historical Bourne shell parsers have accepted without error—but it's the best we have.

셸의 고질적인 문제는, 톰 더프가 Plan 9의 셸인 `rc`에 대한 논문에서 언급했던 것처럼, 아무도 Bourne 셸 문법을 모른다는 것입니다. Posix 셸 위원회는 비록 문맥 의존성이 많지만 유닉스 셸의 결정적 문법을 발표했다는 점에서 그 공을 인정할 필요가 있습니다. 이 문법은, 고전 Bourne 셸 구문 분석기가 오류 없이 지원하던 구성을 지원하지 않는 등 완벽하지는 않지만 우리가 가진 가장 최선의 문법입니다.

The bash parser is derived from an early version of the Posix grammar, and is, as far as I know, the only Bourne-style shell parser implemented using Yacc or Bison. This has presented its own set of difficulties—the shell grammar isn't really well-suited to yacc-style parsing and requires some complicated lexical analysis and a lot of cooperation between the parser and the lexical analyzer.

Bash 구문 분석기는 초기 버전의 Posix 문법에서 기인하였으며, 제가 알기로 Yacc이나 Bison으로 구현된 유일한 Bourn 형식 구문 분석기입니다. Bash 구문 분석기에는 Bash 구문 분석기만의 문제점들이 있습니다. 셸 문법은 yacc 스타일 구문 분석엔 적합하지 않으며, 복잡한 낱말 분석과, 구문 분석기와 낱말 분석기 간의 많은 협력이 필요합니다.

In any event, the lexical analyzer takes lines of input from readline or another source, breaks them into tokens at metacharacters, identifies the tokens based on context, and passes them on to the parser to be assembled into statements and commands. There is a lot of context involved—for instance, the word for can be a reserved word, an identifier, part of an assignment statement, or other word, and the following is a perfectly valid command: that displays `for`.

어쨌거나, 낱말 분석기는 readline이나 다른 곳으로부터 여러 줄의 입력을 받아, 메타 문자를 기준으로 토큰들로 분리하고, 토큰을 문맥에 따라 식별하여 구문 분석기가 선언문과 명령들로 구성할 수 있도록 전달합니다. 이 작업엔 문맥이 많이 개입됩니다. 예를 들어, 단어 for는 예약어, 식별자, 대입문의 일부, 또는 다른 단어일 수도 있습니다. 다음은 `for`를 표시하는 완벽히 유효한 명령입니다:

~~~
for for in for; do for=for; done; echo $for
~~~

At this point, a short digression about aliasing is in order. Bash allows the first word of a simple command to be replaced with arbitrary text using aliases. Since they're completely lexical, aliases can even be used (or abused) to change the shell grammar: it's possible to write an alias that implements a compound command that bash doesn't provide. The bash parser implements aliasing completely in the lexical phase, though the parser has to inform the analyzer when alias expansion is permitted.

이 시점에서, 별칭에 대한 이야기를 잠깐 할까 합니다. Bash는 단순한 명령의 첫번째 단어를 별칭을 사용하여 임의의 문자열로 교체할 수 있게 합니다. 별칭은 완전한 단어이므로, 셸의 문법을 바꾸기 위해 사용(혹은 남용)될 수 있습니다. 별칭을 사용해 bash가 제공하지 않는 컴파운드 명령을 구현하는 것도 가능합니다. 구문 분석기가 언제 별칭을 확장할 수 있는지 낱말 분석기에게 알려 주어야 하지만, Bash 구문 분석기는 낱말 분석 단계에서의 별칭을 완벽히 구현합니다.

Like many programming languages, the shell allows characters to be escaped to remove their special meaning, so that metacharacters such as `&` can appear in commands. There are three types of quoting, each of which is slightly different and permits slightly different interpretations of the quoted text: the backslash, which escapes the next character; single quotes, which prevent interpretation of all enclosed characters; and double quotes, which prevent some interpretation but allow certain word expansions (and treats backslashes differently). The lexical analyzer interprets quoted characters and strings and prevents them from being recognized by the parser as reserved words or metacharacters. There are also two special cases, `$'…'` and `$"…"`, that expand backslash-escaped characters in the same fashion as ANSI C strings and allow characters to be translated using standard internationalization functions, respectively. The former is widely used; the latter, perhaps because there are few good examples or use cases, less so.

다른 프로그래밍 언어들처럼, 셸은 문자열의 특수한 의미를 없애기 위해 예외 문자의 사용을 허용하며, 따라서 `&` 등의 메타문자를 명령에 사용할 수 있습니다. 인용된 문자열의 해석이 조금씩 다른, 세 종류의 인용이 있습니다. 백슬래시는 다음에 오는 문자를 탈출시키며, 작은 따옴표는 감싸는 모든 문자열들의 해석을 방지하고, 쌍따옴표는 몇 종류의 해석을 방지하지만 (백슬래시를 다르게 다루는 동시에) 특정 단어 확장을 허용합니다. 낱말 분석기는 인용된 문자들과 문자열을을 해석하고 구문 분석기에 의해 예약어나 메타문자열로 해석되는 것을 방지합니다. 백슬래시로 탈출된 문자열들을, ANSI C 문자열같은 방식으로, 문자들이 표준 국제화 함수에 의해 번역될 수 있게 확장시키는 두 가지 특수한 경우인 `$'…'` 과 `$"…"`이 있습니다. 전자는 널리 사용되지만, 후자는 용례가 별로 없기 때문에 덜 사용됩니다.

The rest of the interface between the parser and lexical analyzer is straightforward. The parser encodes a certain amount of state and shares it with the analyzer to allow the sort of context-dependent analysis the grammar requires. For example, the lexical analyzer categorizes words according to the token type: reserved word (in the appropriate context), word, assignment statement, and so on. In order to do this, the parser has to tell it something about how far it has progressed parsing a command, whether it is processing a multiline string (sometimes called a "here-document"), whether it's in a case statement or a conditional command, or whether it is processing an extended shell pattern or compound assignment statement.

구문 분석기와 낱말 분석기 간의 나머지 인터페이스는 간단합니다. 구문 분석기는 문법이 요구하는 상태 종속적인 분석을 위해 상태를 인코딩하여 낱말 분석기와 공유합니다. 예를 들어, 낱말 분석기는 토큰 타입에 따라, (적절한 문맥에서) 예약어, 단어, 대입문 등으로 단어를 분류합니다. 이를 위해 구문 분석기는 명령을 얼마나 분석하였는지, ("here-document"로도 불리는) 여러 줄로 이루어진 문자열을 분석하고 있는지, case문이나 조건문을 분석하고 있는지, 아니면 확장된 셸 형태나 컴파운드 대입문을 분석하고 있는지에 대해 알려주어야 합니다.

Much of the work to recognize the end of the command substitution during the parsing stage is encapsulated into a single function (`parse_comsub`), which knows an uncomfortable amount of shell syntax and duplicates rather more of the token-reading code than is optimal. This function has to know about here documents, shell comments, metacharacters and word boundaries, quoting, and when reserved words are acceptable (so it knows when it's in a `case` statement); it took a while to get that right.

구문 분석 단계에서, 명령어 치환의 끝을 알기 위한 대부분의 작업은 하나의 함수(`parse_comsub`)로 감싸여져 있으며, 이 함수는 셸 구문에 대해 불편할 정도로 많이 알고 있으며, 토큰을 읽어들이는 코드의 많은 부분을 중복하여 가집니다. 이 함수는 here document, 셸 주석, 메타문자열, 단어 경계, 인용, 그리고 (`case`문에 있을때 그 사실을 알기 위해)을 예약어를 언제 허용할지에 대한 정보를 알아야 합니다. 이 함수가 올바른 동작을 하는 데에는 굉장히 오랜 시간이 걸렸습니다.

When expanding a command substitution during word expansion, bash uses the parser to find the correct end of the construct. This is similar to turning a string into a command for `eval`, but in this case the command isn't terminated by the end of the string. In order to make this work, the parser must recognize a right parenthesis as a valid command terminator, which leads to special cases in a number of grammar productions and requires the lexical analyzer to flag a right parenthesis (in the appropriate context) as denoting EOF. The parser also has to save and restore parser state before recursively invoking `yyparse`, since a command substitution can be parsed and executed as part of expanding a prompt string in the middle of reading a command. Since the input functions implement read-ahead, this function must finally take care of rewinding the bash input pointer to the right spot, whether bash is reading input from a string, a file, or the terminal using readline. This is important not only so that input is not lost, but so the command substitution expansion functions construct the correct string for execution.

단어 확장 중에 명령어 치환을 확장할 때에, bash는 구조체의 정확한 끝을 알아내기 위해 구문 분석기를 사용합니다. 이것은 문자열을 `eval`을 위한 명령어로 바꾸는 작업과 비슷하지만, 명령이 문자열의 끝으로 끝나지는 않습니다. 이를 위해, 구문 분석기는 오른쪽 괄호를 유효한 명령 종결자로 인식해야 하며, 이것은 낱말 분석기가 (올바른 문맥에서) 오른쪽 괄호를 EOF를 뜻하는 것으로 표시하기를 요구합니다. 또, 구문 분석기는, 명령을 읽어들이는 도중에 프롬프트 문자열 확장의 일환으로 명령 치환이 구문 분석 및 실행될 수 있기 때문에, `yyparse`를 재귀적으로 호출하기 전에 구문 분석기의 상태를 저장하고 복원시켜야 합니다. 입력 함수들이 미리 읽기를 구현하기 때문에, 이 함수는 bash가 입력을 문자열, 파일, 또는 readline을 통한 터미널로부터 읽던 bash 입력 포인터를 올바른 곳으로 되돌려야 합니다. 이것은 입력을 보존하기 위해서 뿐만이 아니라, 명령 치환 확장 함수가 실행될 정확한 문자열을 구성하기 위해서이기도 합니다.

Similar problems are posed by programmable word completion, which allows arbitrary commands to be executed while parsing another command, and solved by saving and restoring parser state around invocations.

프로그래밍 가능한 단어 자동 완성에 의해 다른 명령을 구문 분석하는 도중 임의의 명령을 실행할 수 있게 되는 등 비슷한 문제들이 야기되며, 호출 주변에서 구문 분석기의 상태를 저장하고 복원시킴으로서 해결할 수 있습니다.

Quoting is also a source of incompatibility and debate. Twenty years after the publication of the first Posix shell standard, members of the standards working group are still debating the proper behavior of obscure quoting. As before, the Bourne shell is no help other than as a reference implementation to observe behavior.

인용 역시 상반되는 동작과 논쟁의 이유가 됩니다. 첫 Posix 셸 표준이 발행된 20년 후, 표준 심의회원들은 아직도 모호한 인용에 대한 적절한 작동 방식에 대해 논쟁하고 있습니다. 전과 같이, Bourne 셸은 작동 방식에 대해 관찰할 수 있는 레퍼런스 구현체로서의 가치만을 지닙니다.

The parser returns a single C structure representing a command (which, in the case of compound commands like loops, may include other commands in turn) and passes it to the next stage of the shell's operation: word expansion. The command structure is composed of command objects and lists of words. Most of the word lists are subject to various transformations, depending on their context, as explained in the following sections.

구문 분석기는 하나의 C 구조체를 반환하여(반복문 같은 컴파운드 명령에 경우엔 차례로 다른 명령들을 포함할 수 있습니다), 셸의 다음 작업 단계인 단어 확장을 위해 넘겨줍니다. 명령 구조는 명령 객체와 단어의 목록으로 이루어져 있습니다. 대부분의 단어 목록은, 문맥에 따라, 다음 장에서 설명될 변형들의 대상이 됩니다.

## 3.5. Word Expansions

## 3.5. 단어 확장

After parsing, but before execution, many of the words produced by the parsing stage are subjected to one or more word expansions, so that (for example) $OSTYPE is replaced with the string "linux-gnu".

구문 분석 이후와 실행 이전에, 구문 분석 단계에서 생성된 여러 단어들은 (예를 들어) $OSTYPE이 "linux-gnu"로 치활될 수 있도록 하나 또는 그 이상의 단어 확장의 대상이 됩니다.

### 3.5.1. Parameter and Variable Expansions

### 3.5.1. 매개변수와 변수 확장

Variable expansions are the ones users find most familiar. Shell variables are barely typed, and, with few exceptions, are treated as strings. The expansions expand and transform these strings into new words and word lists.

변수 확장은 사용자들에게 가장 익숙한 확장입니다. 셸 변수들은 극소량의 타입을 사용하며, 몇 가지 예외를 제외하고는 대부분 문자열로 처리됩니다. 확장은 이러한 문자열들을 새로운 단어와 단어 목록으로 변환시킵니다.

There are expansions that act on the variable's value itself. Programmers can use these to produce substrings of a variable's value, the value's length, remove portions that match a specified pattern from the beginning or end, replace portions of the value matching a specified pattern with a new string, or modify the case of alphabetic characters in a variable's value.

변수의 값 자체에 대해 동작하는 확장들이 있습니다. 프로그래머들은 이러한 확장을 이용해 변수의 값, 길이의 부분 문자열을 만들거나, 특정한 형태에 맞는 부분을 제거, 교체하거나, 변수의 값 내의 알파벳들의 대소문자간 변환을 할 수 있습니다.

In addition, there are expansions that depend on the state of a variable: different expansions or assignments happen based on whether or not the variable is set. For instance, `${parameter:-word}` will expand to `parameter` if it's set, and `word` if it's not set or set to the empty string.

또, 변수의 상태에 따라 다르게 동작하는 확장들이 있습니다. 변수가 지정된 여부에 따라 서로 다른 확장이나 대입이 일어나게 할 수 있습니다. 예를 들어, `${parameter:-word}`는 지정되었을 경우 `parameter`로 확장되며, 그렇지 않거나 빈 문자열로 지정되었을땐 `word`로 확장됩니다.

### 3.5.2. And Many More

### 3.5.2. 그리고 더

Bash does many other kinds of expansion, each of which has its own quirky rules. The first in processing order is brace expansion, which turns:

Bash에는 다른 종류의 확장들도 있으며, 각각의 까다로운 규칙을 가집니다. 처리 순서에서 가장 먼저 오는 확장은 중괄호 확장입니다.

    pre{one,two,three}post

into:

를

    preonepost pretwopost prethreepost

로 확장시킵니다.

There is also command substitution, which is a nice marriage of the shell's ability to run commands and manipulate variables. The shell runs a command, collects the output, and uses that output as the value of the expansion.

명령어 치환은 셸의 명령어 실행 기능과 변수 조작 기능의 혼합입니다. 셸이 명령을 실행하고, 출력을 받아, 해당 출력을 확장의 값으로 사용합니다.

One of the problems with command substitution is that it runs the enclosed command immediately and waits for it to complete: there's no easy way for the shell to send input to it. Bash uses a feature named process substitution, a sort of combination of command substitution and shell pipelines, to compensate for these shortcomings. Like command substitution, bash runs a command, but lets it run in the background and doesn't wait for it to complete. The key is that bash opens a pipe to the command for reading or writing and exposes it as a filename, which becomes the result of the expansion.

명령어 치환의 문제점 중 하나는, 감싼 명령어를 즉시 실행시켜 명령이 끝날 때 까지 기다린다는 점이며, 이 때문에 셸이 명령에 입력을 보낼 수 있는 쉬운 방법이 없다는 것입니다. Bash는 이러한 결점을 보완하기 위해, 명령어 치환과 셸 파이프라인의 혼합인, 프로세스 치환이라는 기능을 사용합니다. 명령어 치환처럼 Bash는 명령어를 실행시키지만, 명령을 백그라운드에서 실행시켜, 명령이 끝날 때 까지 기다릴 필요가 없습니다. 프로세스 치환의 핵심은 bash가 명령에 대한 입출력 파이프를 만들고, 확장의 결과가 될 파일명으로 노출하는 것입니다.

Next is tilde expansion. Originally intended to turn `~alan` into a reference to Alan's home directory, it has grown over the years into a way to refer to a large number of different directories.

다음은 물결표 확장입니다. 기존엔 `~alan`을 앨런의 홈 디렉토리에 대한 참조로 변환시키기 위한 의도였지만, 몇 년 간 수많은 다른 디렉토리들에 대한 참조로도 사용할 수 있도록 확장되었습니다.

Finally, there is arithmetic expansion. `$((expression))` causes `expression` to be evaluated according to the same rules as C language expressions. The result of the expression becomes the result of the expansion.

마지막으로, 수식 확장이 있습니다. `$((expression))`는 `expression`이 C 언어 표현식 해석 방식으로 해석되게 합니다. 표현식의 결과물이 확장의 결과가 됩니다.

Variable expansion is where the difference between single and double quotes becomes most apparent. Single quotes inhibit all expansions—the characters enclosed by the quotes pass through the expansions unscathed—whereas double quotes permit some expansions and inhibit others. The word expansions and command, arithmetic, and process substitution take place—the double quotes only affect how the result is handled—but brace and tilde expansion do not.

변수 확장은 따옴표와 쌍따옴표의 차이가 명백히 드러나는 곳입니다. 따옴표는 모든 확장을 억제합니다. 따옴표로 싸여진 문자열들은 아무런 편집이 가해지지 않고 확장 과정을 지나는 반면, 쌍따옴표는 일부 확장은 허용하고 나머지는 억제합니다. 단어 확장과 명령, 수식, 그리고 프로세스 치환이 일어납니다. 쌍따옴표는 결과물이 다뤄지는 방식에만 영향을 미치지만, 중괄호와 물결표는 그렇지 않습니다.

### 3.5.3. Word Splitting

### 3.5.3. 단어 분리

The results of the word expansions are split using the characters in the value of the shell variable `$IFS` as delimiters. This is how the shell transforms a single word into more than one. Each time one of the characters in `$IFS` appears in the result, bash splits the word into two. Single and double quotes both inhibit word splitting.

단어 확장의 결과물은 셸 변수 `$IFS` 값에 있는 문자들을 구분자로서 사용하여 분리됩니다. 이것은 셸이 하나의 단어를 그 이상의 단어들로 변환시키는 방식입니다. `$IFS`에 있는 문자들 중 하나가 결과문에 나타날 때 마다, bash는 해당 단어를 두 개의 단어로 분리시킵니다. 따옴표나 쌍따옴표는 단어 분리를 방지합니다.

### 3.5.4. Globbing

### 3.5.4. 글로빙

After the results are split, the shell interprets each word resulting from the previous expansions as a potential pattern and tries to match it against an existing filename, including any leading directory path.

결과물들이 분리되면, 셸은 이전 확장의 결과물의 각 단어를 잠재적 패턴으로 인식하여, 존재하는 파일의 이름들과 먼저 오는 디렉토리 경로에 대해 매칭합니다.

### 3.5.5. Implementation

### 3.5.5. 구현

If the basic architecture of the shell parallels a pipeline, the word expansions are a small pipeline unto themselves. Each stage of word expansion takes a word and, after possibly transforming it, passes it to the next expansion stage. After all the word expansions have been performed, the command is executed.

셸의 기본적인 설계가 파이프라인에 대응된다면, 단어 확장은 작은 파이프라인으로 볼 수 있습니다. 단어 확장의 각 단계는 단어를 받아, 가능한 변경을 가한 후, 다음 확장 단계에 넘겨 줍니다. 모든 단어 확장들이 수행된 후, 명령이 실행됩니다.

The bash implementation of word expansions builds on the basic data structures already described. The words output by the parser are expanded individually, resulting in one or more words for each input word. The `WORD_DESC` data structure has proved versatile enough to hold all the information required to encapsulate the expansion of a single word. The flags are used to encode information for use within the word expansion stage and to pass information from one stage to the next. For instance, the parser uses a flag to tell the expansion and command execution stages that a particular word is a shell assignment statement, and the word expansion code uses flags internally to inhibit word splitting or note the presence of a quoted null string (`"$x"`, where `$x` is unset or has a null value). Using a single character string for each word being expanded, with some kind of character encoding to represent additional information, would have proved much more difficult.

Bash의 단어 확장 구현은 위에서 설명된 기초 자료 구조를 기반으로 만들어 졌습니다. 구문 분석기에 의해 출력된 단어들은 개별적으로 확장되어, 각 입력 단어당 하나 이상의 단어를 만듭니다. `WORD_DESC` 자료 구조는 단어 하나에 대한 확장의 정보를 포함하는 데 충분히 유연한 것으로 증명되었습니다. 플래그들은 단어 확장 단계와, 단계 간 정보 전달을 위해 사용되는 정보를 인코딩하는 데에 사용됩니다. 예를 들어, 구문 분석기는 플래그를 사용하여 확장과 명령 실행 단계에게 특정 단어가 셸 대입문이라는 것을 알려주며, 단어 확장 코드는 단어 분리를 방지하거나 인용된 널 문자열(`$x`가 지정되지 않았거나 널 값을 가질 때의 `"$x"`)의 존재를 참고하기 위해 내부적으로 플래그를 사용합니다. 추가적인 정보를 나타내기 위한 인코딩을 사용하는, 확장되는 하나의 단어 당 단일 문자로 이루어진 문자열을 사용하는 것은 훨씬 더 힘들었을 것입니다.

As with the parser, the word expansion code handles characters whose representation requires more than a single byte. For example, the variable length expansion (`${#variable}`) counts the length in characters, rather than bytes, and the code can correctly identify the end of expansions or characters special to expansions in the presence of multibyte characters.

구문 분석기와 마찬가지로, 단어 확장 코드 역시 1 바이트 이상을 필요로 하는 문자열들도 다룹니다. 예를 들어, 변수 길이 확장(`${#variable}`)은 길이를 바이트가 아니라 문자 단위로 세며, 해당 작업을 하는 코드는, 멀티바이트 문자열이 존재하는, 확장이나, 확장에 있어 특별한 의미를 가지는 문자열들의 끝을 정확히 판단할 수 있습니다.

## 3.6. Command Execution

## 3.6. 명령 실행

The command execution stage of the internal bash pipeline is where the real action happens. Most of the time, the set of expanded words is decomposed into a command name and set of arguments, and passed to the operating system as a file to be read and executed with the remaining words passed as the rest of the elements of `argv`.

내부 bash 파이프라인의 명령 실행 단계는 진짜 동작이 일어나는 곳입니다. 대부분의 경우, 확장된 단어들의 집합은 명령의 이름과 매개 변수의 집합으로 분해되며, 읽고 실행할 파일과, 그 나머지 단어들을 `argv`의 요소로서, 운영체제에게 전달됩니다.

The description thus far has deliberately concentrated on what Posix calls simple commands—those with a command name and a set of arguments. This is the most common type of command, but bash provides much more.

지금까지는 일부러 Posix가 단순한 명령으로 부르는, 명령 이름과 매개 변수의 집합을 가진 것들에 집중하였습니다. 이 명령들은 가장 흔한 종류의 명령이지만, bash는 그 이상을 제공합니다.

The input to the command execution stage is the command structure built by the parser and a set of possibly-expanded words. This is where the real bash programming language comes into play. The programming language uses the variables and expansions discussed previously, and implements the constructs one would expect in a high-level language: looping, conditionals, alternation, grouping, selection, conditional execution based on pattern matching, expression evaluation, and several higher-level constructs specific to the shell.

명령 실행 단계로의 입력은 구문 분석기에 의해 만들어진 명령 구조와 확장되었을 수도 있는 단어의 집합입니다. 이곳은 bash 프로그래밍 언어가 빛을 발하는 곳입니다. Bash 프로그래밍 언어는 위에서 언급된 변수와 확장을 사용하여, 고수준 언어에서 기대할 수 있는 반복문, 변형, 그룹, 패턴 매칭을 기반으로 한 조건 실행문, 표현식 평가, 그리고 몇 가지 셸에 종속적인 고수준 구문 등의 구문들을 구현합니다.

### 3.6.1. Redirection

### 3.6.1. 리다이렉션

One reflection of the shell's role as an interface to the operating system is the ability to redirect input and output to and from the commands it invokes. The redirection syntax is one of the things that reveals the sophistication of the shell's early users: until very recently, it required users to keep track of the file descriptors they were using, and explicitly specify by number any other than standard input, output, and error.

운영 체제로의 인터페이스로서의 셸의 역할의 반영 중 하나는 셸이 실행하는 명령의 입력과 출력을 리다이렉트 하는 기능입니다. 리다이렉션 구문은 셸의 초기 사용자들의 세련됨을 보여주는 것들 중 하나입니다. 아주 최근까지, 사용자들이 사용하는 파일 서술자들을 직접 관리하고, 표준 입출력과 에러 외의 것들을 숫자로 명시적으로 지정할 것을 요구했습니다.

A recent addition to the redirection syntax allows users to direct the shell to choose a suitable file descriptor and assign it to a specified variable, instead of having the user choose one. This reduces the programmer's burden of keeping track of file descriptors, but adds extra processing: the shell has to duplicate file descriptors in the right place, and make sure they are assigned to the specified variable. This is another example of how information is passed from the lexical analyzer to the parser through to command execution: the analyzer classifies the word as a redirection containing a variable assignment; the parser, in the appropriate grammar production, creates the redirection object with a flag indicating assignment is required; and the redirection code interprets the flag and ensures that the file descriptor number is assigned to the correct variable.

리다이렉션 문법에 최근에 추가된 것은, 사용자들이 관리하는 것이 아닌, 셸이 직접 적합한 파일 서술자를 고르고 지정된 변수에 할당시키게 하는 것입니다. 이것을 프로그래머가 파일 서술자들을 관리하는 것의 부담을 덜어주지만, 추가적인 처리를 요구합니다: 셸은 파일 서술자를 올바른 곳에 복사해야 하며, 특정 변수에 할당되어 있다는 것을 보장해야 합니다. 이것은 낱말 분석기에서 구문 분석기, 그리고 명령 실행으로 정보가 전달되는 예시 중 하나입니다. 분석기는 단어를 변수 할당을 포함하는 리다이렉션으로 분류합니다; 구문 분석기는, 적절한 문법 프로덕션의 문맥에서, 할당을 요한다는 사실을 알리는 플래그를 가진 리다이렉션 객체를 만들고, 리다이렉션 코드는 플래그를 해석하여 파일 서술자 번호가 올바른 변수에 할당되어 있는지 보장하게 됩니다.

The hardest part of implementing redirection is remembering how to undo redirections. The shell deliberately blurs the distinction between commands executed from the filesystem that cause the creation of a new process and commands the shell executes itself (builtins), but, no matter how the command is implemented, the effects of redirections should not persist beyond the command's completion2. The shell therefore has to keep track of how to undo the effects of each redirection, otherwise redirecting the output of a shell builtin would change the shell's standard output. Bash knows how to undo each type of redirection, either by closing a file descriptor that it allocated, or by saving file descriptor being duplicated to and restoring it later using `dup2`. These use the same redirection objects as those created by the parser and are processed using the same functions.

리다이렉션을 구현하는 데에 있어서 가장 어려운 부분은 리다이렉션을 취소하는 방법을 기억하는 것입니다. 셸은, 새로운 프로세스를 생성하는, 파일 시스템에서부터 실행된 명령들과, 셸 자체적으로 실행하는 프로세스(빌트인)의 구분을, 일부러 모호하게 하지만, 명령이 어떻게 구현되었든 간에, 리다이렉션의 효과는 명령이 끝난 이후에 남아있어선 안됩니다. 따라서, 셸은 각 리다이렉션의 영향을 되돌리는 방법을 알고 있어야 하며, 그렇지 않을 경우 셸 빌트인의 출력을 리다이렉트 하는 것은 셸의 표준 출력을 변경시킬 것입니다. Bash는, 리다이렉션이 할당한 파일 서술자를 닫거나, 복사되는 파일 서술자를 저장하고 추후에 `dup2`을 사용하여 복원하는 등, 각 종류의 리다이렉션을 되돌리는 방법을 알고 있습니다. 이 작업들은 구문 분석기가 생성하는 것들과 같은 리다이렉션 객체를 사용하며, 같은 함수를 사용하여 처리됩니다.

Since multiple redirections are implemented as simple lists of objects, the redirections used to undo are kept in a separate list. That list is processed when a command completes, but the shell has to take care when it does so, since redirections attached to a shell function or the "`.`" builtin must stay in effect until that function or builtin completes. When it doesn't invoke a command, the `exec` builtin causes the undo list to simply be discarded, because redirections associated with `exec` persist in the shell environment.

다중 리다이렉션이 단순히 객체의 목록으로 구현되어 있기 때문에, 되돌리기 위한 리다이렉션들은 별도의 목록에 저장하게 됩니다. 이 목록은 명령이 종료되었을 때 처리되지만, 셸 함수나 "`.`" 빌트인에 연결되어 있는 리다이렉션들은 해당 함수나 빌트인이 끝날 때 까지 유효해야 하므로, 셸은 이 처리가 언제 일어나는지 대해 주의를 요해야 합니다. 명령을 실행시키지 않으면, `exec`와 연관된 리다이렉션들은 셸 환경에 보존되어 있기 때문에 `exec` 빌트인은 되돌리기 목록을 폐기합니다. 

The other complication is one bash brought on itself. Historical versions of the Bourne shell allowed the user to manipulate only file descriptors 0-9, reserving descriptors 10 and above for the shell's internal use. Bash relaxed this restriction, allowing a user to manipulate any descriptor up to the process's open file limit. This means that bash has to keep track of its own internal file descriptors, including those opened by external libraries and not directly by the shell, and be prepared to move them around on demand. This requires a lot of bookkeeping, some heuristics involving the close-on-exec flag, and yet another list of redirections to be maintained for the duration of a command and then either processed or discarded.

또 다른 복잡함은 bash가 스스로 짊어진 부담입니다. 고전 Bourne 셸은 사용자가 0번부터 9번까지의 파일 서술만을 조작할 수 있게 했으며, 10번 이상의 파일 서술자들은 셸 내부에서의 사용을 위해 예약하였습니다. Bash는 이 제한을 풀었으며, 사용자가 프로세스가 열 수 있는 파일의 한계치만큼의 서술자를 조작할 수 있게 하였습니다. 이것의 의미는, bash가 직접 열지 않은, 외부 라이브러리들이 연 파일 서술자들을 관리하고, 요청에 따라 서술자들을 이동시킬 수 있어야 합니다. 이것은 많은 관리를 요하며, close-on-exec 플래그가 관련되는 휴리스틱, 그리고 명령이 실행되는 동안 관리되어야 하고, 명령이 끝나면 폐기하거나 처리할 또다른 리다이렉션의 목록이 생깁니다.

### 3.6.2. Builtin Commands

### 3.6.2. 빌트인 명령

Bash makes a number of commands part of the shell itself. These commands are executed by the shell, without creating a new process.

Bash는 셸의 일부인 몇 가지 명령들을 만듭니다. 이 명령들은 새로운 프로세스를 만들지 않으면서 셸에 의해 실행됩니다.

The most common reason to make a command a builtin is to maintain or modify the shell's internal state. `cd` is a good example; one of the classic exercises for introduction to Unix classes is to explain why `cd` can't be implemented as an external command.

명령을 빌트인으로 만드는 가장 흔한 이유는 셸의 내부 상태를 유지하거나 조작하기 위해서입니다. `cd`는 유닉스 입문 수업에서 `cd`가 외부 명령으로 구현될 수 없는 이유를 설명하기 위한 빌트인의 좋은 예시입니다.

Bash builtins use the same internal primitives as the rest of the shell. Each builtin is implemented using a C language function that takes a list of words as arguments. The words are those output by the word expansion stage; the builtins treat them as command names and arguments. For the most part, the builtins use the same standard expansion rules as any other command, with a couple of exceptions: the bash builtins that accept assignment statements as arguments (e.g., `declare` and `export`) use the same expansion rules for the assignment arguments as those the shell uses for variable assignments. This is one place where the `flags` member of the `WORD_DESC` structure is used to pass information between one stage of the shell's internal pipeline and another.

Bash 빌트인들은 셸의 다른 부분과 같은 내부 기본형을 사용합니다. 각 빌트인은 C 언어의 함수들을 사용하여 구현되어 있습니다. 단어들은 단어 확장 단계에서 출력된 단어들이며, 빌트인들은 이 단어들을 명령 이름과 매개 변수로 취급합니다. 대부분의 경우, 빌트인들은 두 개의 예외를 제외하고는 다른 명령들에 적용되는 것과 같은 표준 확장 규칙이 적용됩니다. 대입문을 매개 변수로 받는 bash 빌트인들(`declare`, `export` 등)은 셸이 변수 할당에 사용되는 같은 확장 규칙이 적용됩니다. 이곳은 `WORD_DESC` 구조체의 `flags` 멤버가 셸의 내부 파이프라인의 단계 간 정보를 전달하기 위해 사용되는 곳입니다.

### 3.6.3. Simple Command Execution

### 3.6.3. 단순한 명령 실행

Simple commands are the ones most commonly encountered. The search for and execution of commands read from the filesystem, and collection of their exit status, covers many of the shell's remaining features.

단순한 명령들은 가장 흔히 마주치게 되는 명령입니다. 파일시스템으로부터 읽어들인 명령들의 검색과 실행, 그리고 반환값의 수집은 셸의 수많은 나머지 기능들을 포함합니다.

Shell variable assignments (i.e., words of the form `var=value`) are a kind of simple command themselves. Assignment statements can either precede a command name or stand alone on a command line. If they precede a command, the variables are passed to the executed command in its environment (if they precede a built-in command or shell function, they persist, with a few exceptions, only as long as the builtin or function executes). If they're not followed by a command name, the assignment statements modify the shell's state.

셸 변수 할당(`var=value`의 형태를 가지는 단어)은 이 자체로 단순한 명령입니다. 대입문들은 커맨드 라인에서 명령 앞에 오거나 단독적으로 존재할 수 있습니다. 대입문이 명령 앞에 올 땐, 변수들은 (빌트인 명령이나 셸 명령 앞에 올 땐, 몇 가지 예외를 제외하고는, 빌트인이나 함수가 실행되는 도중에는 영속됩니다) 각자의 환경 내에서, 실행된 명령에 전달됩니다. 그렇지 않을 때에 대입문은 셸의 상태를 변경시킵니다.

When presented a command name that is not the name of a shell function or builtin, bash searches the filesystem for an executable file with that name. The value of the `PATH` variable is used as a colon-separated list of directories in which to search. Command names containing slashes (or other directory separators) are not looked up, but are executed directly.

셸 함수나 빌트인이 아닌 명령이 주어졌을 때엔, bash는 파일 시스템에서 그 명령의 이름을 가진 실행 가능한 파일을 검색합니다. `PATH` 변수의 값은 검색할 디렉토리들을 쌍점으로 구분하여 가집니다. 사선(또는 다른 디렉토리 구분자)이 들어가 있는 명령들은 검색되지 않고 바로 실행됩니다.

When a command is found using a `PATH` search, bash saves the command name and the corresponding full pathname in a hash table, which it consults before conducting subsequent PATH searches. If the command is not found, bash executes a specially-named function, if it's defined, with the command name and arguments as arguments to the function. Some Linux distributions use this facility to offer to install missing commands.

명령이 `PATH` 검색을 통해 발견되면, bash는 명령 이름과 해당되는 절대경로를 저장하고, 다음 `PATH` 검색에 참고합니다. 명령을 찾을 수 없는 경우, bash는, 정의되어 있는 경우, 특별한 이름을 가진 함수를, 명령 이름과 매개 변수들을 함수의 매개 변수로 넘겨 실행합니다. 일부 리눅스 배포판들은 이 기능을, 없는 명령의 설치를 제안하기 위해 사용합니다.

If bash finds a file to execute, it forks and creates a new execution environment, and executes the program in this new environment. The execution environment is an exact duplicate of the shell environment, with minor modifications to things like signal disposition and files opened and closed by redirections.

Bash가 실행할 파일을 찾을 경우, 포크 후 새로운 실행 환경을 만들고, 명령을 이 새로운 환경에서 실행합니다. 실행 환경은, 시그널 처리와 리다이렉션에 의해 열리거나 닫힌 파일들에 대한 사소한 수정 사항을 제외하고는, 셸 환경의 완벽한 사본입니다.

### 3.6.4. Job Control

### 3.6.4. 작업 제어

The shell can execute commands in the foreground, in which it waits for the command to finish and collects its exit status, or the background, where the shell immediately reads the next command. Job control is the ability to move processes (commands being executed) between the foreground and background, and to suspend and resume their execution. To implement this, bash introduces the concept of a job, which is essentially a command being executed by one or more processes. A pipeline, for instance, uses one process for each of its elements. The process group is a way to join separate processes together into a single job. The terminal has a process group ID associated with it, so the foreground process group is the one whose process group ID is the same as the terminal's.

셸은 명령이 끝날 때 까지 기다리다가 반환값을 수집하는 전경 실행과, 바로 다음 명령을 읽어들이는 배경 실행을 할 수 있습니다. 작업 제어는 프로세스들을 전경과 배경간 전환하고, 실행을 보류, 재개할 수 있는 기능입니다. 이것을 구현하기 위해, bash는, 본질적으로는, 하나 이상의 프로세스들로 실행되는 명령인, 작업이라는 개념을 도입합니다. 예를 들어, 파이프라인은 각 요소에 대해 하나의 프로세스를 사용합니다. 터미널은 터미널에 연관된 프로세스 그룹 ID를 가지므로, 전경 프로세스 그룹은 터미널과 같은 프로세스 그룹 ID를 가진 그룹입니다. 

The shell uses a few simple data structures in its job control implementation. There is a structure to represent a child process, including its process ID, its state, and the status it returned when it terminated. A pipeline is just a simple linked list of these process structures. A job is quite similar: there is a list of processes, some job state (running, suspended, exited, etc.), and the job's process group ID. The process list usually consists of a single process; only pipelines result in more than one process being associated with a job. Each job has a unique process group ID, and the process in the job whose process ID is the same as the job's process group ID is called the process group leader. The current set of jobs is kept in an array, conceptually very similar to how it's presented to the user. The job's state and exit status are assembled by aggregating the state and exit statuses of the constituent processes.

셸은 작업 제어를 구현하기 위해 몇 가지 간단한 자료 구조를 사용합니다. 프로세스 ID, 상태, 종료되었을 때의 상황을 포함하는, 자식 프로세스를 나타내는 구조체가 있습니다. 파이프라인은 단순히 이러한 프로세스 구조의 연결 리스트입니다. 작업은 이것과 비슷합니다. 프로세스 목록, 작업 상태(실행 중, 보류됨, 끝남 등), 그리고 작업의 프로세스 그룹 ID가 있습니다. 프로세스 목록은 주로 하나의 프로세스로만 이루어져 있습니다. 오직 파이프라인들만이 하나의 작업에 그 이상의 프로세스가 연관되게 됩니다. 각 작업은 고유한 프로세스 그룹 ID를 가지며, 작업의 프로세스 그룹 ID와 같은 프로세스 ID를 가지는 프로세스는 프로세스 그룹 리더라고 불립니다. 현재 작업들은 배열에 저장되어 있으며, 이것은 사용자들에게 보이는 것과 개념적으로 매우 비슷합니다. 작업의 상태와 종료 상황들은, 작업을 이루는 프로세스들의 상태와 반환값들을 모아 만들어집니다.

Like several other things in the shell, the complex part about implementing job control is bookkeeping. The shell must take care to assign processes to the correct process groups, make sure that child process creation and process group assignment are synchronized, and that the terminal's process group is set appropriately, since the terminal's process group determines the foreground job (and, if it's not set back to the shell's process group, the shell itself won't be able to read terminal input). Since it's so process-oriented, it's not straightforward to implement compound commands such as while and for loops so an entire loop can be stopped and started as a unit, and few shells have done so.

셸의 다른 것들과 비슷하게, 작업 제어를 구현하는 것의 복잡한 부분은 이것이 많은 관리를 요구한다는 것입니다. 셸은 프로세스들을 올바른 프로세스 그룹에 할당하고, 자식 프로세스 생성과 프로세스 그룹 할당이 동기적으로 일어나며, 터미널의 프로세스 그룹이 전경 작업을 결정하기 때문에 (또, 셸의 프로세스 그룹으로 다시 재설정되지 않으면, 셸은 터미널 입력을 읽을 수 없기 때문에), 터미널의 프로세스 그룹이 올바르게 설정되어 있는 지 확인해야 합니다. 작업 제어는 매우 프로세스 지향적이기 때문에, 반복문 통째로 하나의 단위로서 멈추고 재개시킬 수 있도록, while이나 for 반복문 같은 컴파운드 명령을 구현하는 것이 간단하지 않기 때문에, 구현하는 셸이 별로 없습니다.

### 3.6.5. Compound Commands

### 3.6.5. 컴파운드 명령

Compound commands consist of lists of one or more simple commands and are introduced by a keyword such as `if` or `while`. This is where the programming power of the shell is most visible and effective.

컴파운드 명령은 하나 이상의 단순한 명령의 목록으로 이루져 있으며, `if`나 `while` 등의 키워드로 도입됩니다. 컴파운드 명령은 셸 프로그래밍의 강력함이 가장 잘 나타나고 효과적인 곳입니다.

The implementation is fairly unsurprising. The parser constructs objects corresponding to the various compound commands, and interprets them by traversing the object. Each compound command is implemented by a corresponding C function that is responsible for performing the appropriate expansions, executing commands as specified, and altering the execution flow based on the command's return status. The function that implements the `for` command is illustrative. It must first expand the list of words following the `in` reserved word. The function must then iterate through the expanded words, assigning each word to the appropriate variable, then executing the list of commands in the `for` command's body. The for command doesn't have to alter execution based on the return status of the command, but it does have to pay attention to the effects of the `break` and `continue` builtins. Once all the words in the list have been used, the `for` command returns. As this shows, for the most part, the implementation follows the description very closely.

컴파운드 명령의 구현은 딱히 놀랄 것이 못 됩니다. 구문 분석기는 컴파운드 명령에 대응하는 객체들을 만들고, 객체를 탐색하여 해석합니다. 각 컴파운드 명령은, 적절한 확장을 수행, 지정된 명령의 실행, 그리고 명령의 반환값에 따라 실행 흐름을 조작하는 것을 담당하는 C 함수에 의해 구현됩니다. `for` 명령을 구현하는 함수를 예로 들어 보겠습니다. 이 함수는 먼저 예약어인 `in` 다음에 오는 단어의 목록을 확장합니다. 이 함수는 또, 확장된 단어들을 돌아가며 각 단어를 적절한 변수에 할당하고, `for` 명령 내의 명령 목록을 실행합니다. for 명령은, 명령의 반환값에 따라 실행을 조작하지 않아도 되지만, `break`와 `continue` 빌트인의 효과에 대해서는 주의를 해야 합니다. 목록에 있는 모든 단어들이 사용되면, `for` 명령이 반환됩니다. 이것이 보여주는 것 처럼, 대부분의 경우, 구현은 설명과 매우 유사하게 동작합니다.

## 3.7. Lessons Learned

## 3.7. 얻은 교훈

### 3.7.1. What I Have Found Is Important

### 3.7.1. 내가 알아낸 것은 중요하다

I have spent over twenty years working on bash, and I'd like to think I have discovered a few things. The most important—one that I can't stress enough—is that it's vital to have detailed change logs. It's good when you can go back to your change logs and remind yourself about why a particular change was made. It's even better when you can tie that change to a particular bug report, complete with a reproducible test case, or a suggestion.

저는 bash에 대한 작업을 20년 이상 해 왔으며, 몇 가지 사실을 발견했다고 생각하고 싶습니다. 아무리 강조해도 충분하지 않은, 제일 중요한 것은, 자세한 체인지로그는 필수적이라는 것입니다. 체인지로그로 돌아가 특정 변경 사항에 대한 결정이 왜 일어났는지에 대해 상기할 수 있다는 것은 좋은 일입니다. 해당 변경 사항을 재현 가능한 테스트 케이스나 제안과 함께 있는 특정 버그 리포트에 연결할 수 있을 경우 더 좋습니다.

If it's appropriate, extensive regression testing is something I would recommend building into a project from the beginning. Bash has thousands of test cases covering virtually all of its non-interactive features. I have considered building tests for interactive features—Posix has them in its conformance test suite—but did not want to have to distribute the framework I judged it would need.

적절하다면, 포괄적인 회귀 테스트는 프로젝트의 시작부터 넣는 것을 추천하고 싶습니다. Bash엔 Bash의 사실상 모든 비대화적인 기능을 다루는 대한 수천개의 테스트 케이스가 있습니다. 대화적인 기능에 대한 테스트를 만드는 것을 고려해 보았지만(Posix에 부합 테스트 모음이 있긴 합니다), 테스트 모음이 필요로 할 것으로 판단한 프레임워크를 배포하기 싫었습니다.

Standards are important. Bash has benefited from being an implementation of a standard. It's important to participate in the standardization of the software you're implementing. In addition to discussions about features and their behavior, having a standard to refer to as the arbiter can work well. Of course, it can also work poorly—it depends on the standard.

표준은 중요합니다. Bash는 표준 구현체로서의 혜택을 받았습니다. 당신이 구현하고 있는 소프트웨어의 표준화에 참여하는 것은 중요합니다. 소프트웨어의 기능과 동작에 대한 토론은 물론, 중재인으로서의 표표준을 가지고 있는 것도 잘 동작할 수 있습니다. 물론, 표준에 따라, 형편없이 동작할 수도 있습니다.

External standards are important, but it's good to have internal standards as well. I was lucky enough to fall into the GNU Project's set of standards, which provide plenty of good, practical advice about design and implementation.

외부 표준도 중요하지만, 내부 표준도 가지는 것도 좋습니다. 나는 설계와 구현에 대한 충분한 양의 훌륭하고, 실용적인 조언을 제공받을 수 있는, GNU 프로젝트의 표준에 들어가기에 운이 좋았습니다.

Good documentation is another essential. If you expect a program to be used by others, it's worth having comprehensive, clear documentation. If software is successful, there will end up being lots of documentation for it, and it's important that the developer writes the authoritative version.

좋은 문서는 또 다른 필수 요소입니다. 어떤 프로그램이 다른 사용자에 의해 사용될 것이라고 생각한다면, 포괄적이고 명확한 문서는 그 가치를 합니다. 해당 소프트웨어가 성공적이면, 그 소프트웨어에 대한 많은 문서들이 생겨날 것이며, 개발자가 권위 있는 버전의 문서를 쓰는 것이 중요합니다.

There's a lot of good software out there. Use what you can: for instance, gnulib has a lot of convenient library functions (once you can unravel them from the gnulib framework). So do the BSDs and Mac OS X. Picasso said "Great artists steal" for a reason.

세상에는 많은 좋은 소프트웨어들이 있습니다. 쓸 수 있는 것을 쓰십시오. 예를 들어, gnulib은 수많은 편리한 라이브러리 함수를 가지고 있습니다. BSD와 Mac OS X도 마찬가지입니다. 피카소가 "위대한 예술가들은 훔친다"라는 말을 괜히 한 것이 아닙니다.

Engage the user community, but be prepared for occasional criticism, some that will be head-scratching. An active user community can be a tremendous benefit, but one consequence is that people will become very passionate. Don't take it personally.

사용자 커뮤니티와 소통하는 동시에, 종종 있는 비판에 준비되어 있으십시오. 일부는 의문을 가지게 할 것입니다. 활성화된 사용자 커뮤니티는 매우 큰 도움이 될 수 있지만, 그것은 사용자들을 매우 격렬하게 만들기도 합니다. 개인적으로 받아들이지 마세요.

### 3.7.2. What I Would Have Done Differently

### 3.7.2. 다르게 하고 싶었던 것들

Bash has millions of users. I've been educated about the importance of backwards compatibility. In some sense, backwards compatibility means never having to say you're sorry. The world, however, isn't quite that simple. I've had to make incompatible changes from time to time, nearly all of which generated some number of user complaints, though I always had what I considered to be a valid reason, whether that was to correct a bad decision, to fix a design misfeature, or to correct incompatibilities between parts of the shell. I would have introduced something like formal bash compatibility levels earlier.

Bash는 수백만명의 사용자 층을 가지고 있습니다. 하위 호환성의 중요성에 대해서는 알고 있습니다. 어떤 관점에서는, 하위 호환성은 미안해야 할 일이 없다는 것을 의미하기도 합니다. 하지만, 세상은 그렇게 단순하지 않습니다. 종종 호환되지 않는 변경점들을 만들어야 할 때도 있으며, 이 변경점 대부분들은 일부 사용자의 불만을 야기했지만, 제가 생각하기엔, 그 결정이 옮은 결정이든 잘못된 결정이든, 설계 실수를 고치기 위해서든, 셸의 영역 간 비호환성을 고치기 위해서였든, 언제나 타당한 이유를 가지고 있었습니다. 좀 더 일찍 정식 bash 호환성 단계를 만들어 놨었으면 합니다.

Bash's development has never been particularly open. I have become comfortable with the idea of milestone releases (e.g., bash-4.2) and individually-released patches. There are reasons for doing this: I accommodate vendors with longer release timelines than the free software and open source worlds, and I've had trouble in the past with beta software becoming more widespread than I'd like. If I had to start over again, though, I would have considered more frequent releases, using some kind of public repository.

Bash의 개발은 딱히 투명하진 않았습니다. 저는 마일스톤 릴리즈(bash-4.2 등)와, 개인이 릴리즈하는 패치의 개념에 익숙해져 있었습니다. 이렇게 한 이유가 있습니다. 자유 소프트웨어와 오픈 소스 세상보다 긴 릴리즈 타임라인을 가진 벤더들의 사정에도 맞춰 줘야 했으며, 과거에 원하던 것 이상 베타 버전의 소프트웨어가 광범위하게 확산되어 문제를 겪었던 적이 많았기 때문입니다. 하지만, 새로 시작할 수 있다면, 공개 저장소를 사용하여, 릴리즈를 좀 더 자주 하였을 것입니다.

No such list would be complete without an implementation consideration. One thing I've considered multiple times, but never done, is rewriting the bash parser using straight recursive-descent rather than using `bison`. I once thought I'd have to do this in order to make command substitution conform to Posix, but I was able to resolve that issue without changes that extensive. Were I starting bash from scratch, I probably would have written a parser by hand. It certainly would have made some things easier.

구현에 대한 고려 사항 없이는 이 목록은 허전할 것입니다. 여러 번 생각만 하고 실제로 하지 못했던 것들 중 하나는, bash 구문 분석기를 `bison` 대신, 알기 쉬운, 되부름 하향 구문 분석 방식으로 다시 작성하는 것입니다. 한때는 명령 치환 기능을 Posix 표준에 맞추기 위해 이런 작업을 해야 할 줄 알았지만, 이렇게 큰 변경 사항을 만들지 않고서도 해낼 수 있었습니다. Bash를 처음부터 구현한다면, 직접 손으로 구문 분석기를 짰을 것입니다. 그랬다면 여러 가지가 쉬워졌을 것입니다.

## 3.8. Conclusions

## 3.8. 결론

Bash is a good example of a large, complex piece of free software. It has had the benefit of more than twenty years of development, and is mature and powerful. It runs nearly everywhere, and is used by millions of people every day, many of whom don't realize it.

Bash는 크고 복잡한 자유 소프트웨어의 좋은 예입니다. 20년 이상의 개발 시간이라는 혜택을 가지고 있으며, 성숙하고 강력합니다. 거의 모든 곳에서 작동하며, Bash를 사용한다는 것을 인식하지 못하는 다수를 포함해, 매일 수백만명의 사람들이 사용합니다. 

Bash has been influenced by many sources, dating back to the original 7th Edition Unix shell, written by Stephen Bourne. The most significant influence is the Posix standard, which dictates a significant portion of its behavior. This combination of backwards compatibility and standards compliance has brought its own challenges.

Bash는 Stephen Bourne가 작성한 7th Edition 유닉스 셸부터, 많은 기존 프로젝트들의 영향을 받았습니다. Bash에 가장 큰 영향은 미친 건, Bash의 동작의 상당한 부분을 정의한 Posix 표준이었습니다. 이러한 하위 호환성과 표준 준수의 조합은 그 나름대로의 도전이 있었습니다.

Bash has profited by being part of the GNU Project, which has provided a movement and a framework in which bash exists. Without GNU, there would be no bash. Bash has also benefited from its active, vibrant user community. Their feedback has helped to make bash what it is today—a testament to the benefits of free software.

Bash는 GNU 프로젝트로서의 일부로서, Bash가 존재하는 기반이 되는 동기와 체제를 제공받는 이점을 얻었습니다. GNU가 없었으면 bash도 없었을 것입니다. Bash는 적극적인 사용자 커뮤니티의 혜택도 받았습니다. 사용자들의 의견은 지금까지의 bash를 만들어 왔습니다. 이것은 자유 소프트웨어로서의 이점의 증거입니다.
