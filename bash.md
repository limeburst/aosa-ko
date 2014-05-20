## 3.1. Introduction

## 3.1. 서론

A Unix shell provides an interface that lets the user interact with the operating system by running commands. But a shell is also a fairly rich programming language: there are constructs for flow control, alternation, looping, conditionals, basic mathematical operations, named functions, string variables, and two-way communication between the shell and the commands it invokes.

유닉스 셸은 명령을 실행하는 방식으로 사용자들에게 운영체제와 상호 작용하기 위한 인터페이스를 제공한다. 하지만 셸은 꽤나 풍부한 프로그래밍 언어이기도 하다. 그 예시로, 셸은 흐름 제어, 반복문, 조건문, 기본적인 연산, 기명 함수, 문자열 변수, 그리고 셸과 실행되는 명령 간의 통신을 위한 구문를 제공한다.

Shells can be used interactively, from a terminal or terminal emulator such as xterm, and non-interactively, reading commands from a file. Most modern shells, including bash, provide command-line editing, in which the command line can be manipulated using emacs- or vi-like commands while it's being entered, and various forms of a saved history of commands.

셸은 xterm 등의 터미널 에뮬레이터를 통해 대화식으로 사용하거나, 파일을 통해 명령을 전달하는 비대화식으로도 사용할 수 있다. bash를 포함하여 대부분의 현대적인 셸은 커맨드 라인을 emacs나 vi의 키 바인딩을 통해 편집할 수 있으며, 여러 형태로 과거에 실행하였던 명령들을 저장하여 제공한다.

Bash processing is much like a shell pipeline: after being read from the terminal or a script, data is passed through a number of stages, transformed at each step, until the shell finally executes a command and collects its return status.

Bash의 데이터 처리 방식은 셸 파이프라인과 비슷하다. 데이터는 터미널이나 스크립트를 통해 읽어진 다음, 셸이 명령을 실행하고 리턴값을 받아 오게 될 까지 몇 단계를 거쳐 변형되는 과정을 거친다.

This chapter will explore bash's major components: input processing, parsing, the various word expansions and other command processing, and command execution, from the pipeline perspective. These components act as a pipeline for data read from the keyboard or from a file, turning it into an executed command.

이번 장에서는 파이프라인의 관점에서 bash의 입력 처리, 파싱, 단어 단위 확장, 그리고 명령 실행까지의 구성 요소를 파악할 것이다. 이러한 구성 요소들은 키보드나 파일로부터 읽어들이는 데이터를 실행 가능한 명령으로 바꾸기 위한 파이프라인의 역할을 한다.

### 3.1.1. Bash

### 3.1.1. Bash

Bash is the shell that appears in the GNU operating system, commonly implemented atop the Linux kernel, and several other common operating systems, most notably Mac OS X. It offers functional improvements over historical versions of sh for both interactive and programming use.

Bash는 리눅스 커널 기반으로 구현된 GNU 운영체제와 몇몇 다른 일반적인 운영체제, 특히 OS X에 탑재되어 있는 셸이다. 대화식 사용은 물론 프로그래밍 용도에서도 sh에 비해 기능적인 개선사항을 제공한다.

The name is an acronym for Bourne-Again SHell, a pun combining the name of Stephen Bourne (the author of the direct ancestor of the current Unix shell /bin/sh, which appeared in the Bell Labs Seventh Edition Research version of Unix) with the notion of rebirth through reimplementation. The original author of bash was Brian Fox, an employee of the Free Software Foundation. I am the current developer and maintainer, a volunteer who works at Case Western Reserve University in Cleveland, Ohio.

Bash의 이름은 Stephen Bourne(현 유닉스 셸인 /bin/sh의, Bell Labs의 일곱번째 에디션 유닉스의 연구용 버전에서 처음 등장한, 직속 조상 프로그램의 개발자이다.)의 이름과 재구현을 통한 재탄생의 개념을 합친 말장난인 Bourne-Again SHell의 두문자어이다. bash의 원저작자는 Free Software Foundation의 직원인 Brian Fox이며, 지금은 Cleveland, Ohio에 있는 Base Western Reserve University 에서 자원 봉사 일을 하고 있는 내가 개발과 유지를 맡고 있다.

Like other GNU software, bash is quite portable. It currently runs on nearly every version of Unix and a few other operating systems—independently-supported ports exist for hosted Windows environments such as Cygwin and MinGW, and ports to Unix-like systems such as QNX and Minix are part of the distribution. It only requires a Posix environment to build and run, such as one provided by Microsoft's Services for Unix (SFU).

다른 GNU 소프트웨어처럼, bash는 꽤나 포터블하다. 현재 거의 모든 버전의 유닉스에서 작동하며, Cygwin이나 MinGW처럼 윈도우 호스트 환경에서 자체적으로 포팅한 버전이 존재하며, QNX와 Minix 같은 Unix-like 운영체제를 위해 포팅된 버전도 함께 배포한다. Microsoft's Services for Unix(SFU)에서 제공하는 환경처럼 Posix 환경만 있으면 빌드 및 실행할수 있다.
