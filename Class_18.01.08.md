18.01.08 MON

GOAL
컴퓨터를 이행하고 메모리 구조체계에 대해 이해할 수 있다.
Computational Thinking을 이해하고 실생활에 적용할 수 있다.
프로그래밍에 대한 전반적인 이해를 할 수 있다. 

**1. Understanding of computer systems**

**1.1 What is Computer?**

compute + er: 계산하는 기계
Computation vs Calculation
“calculation” implies a strictly arithmetic process(산술과정), whereas “computation” might involve applying rules in a systematic way.

**Computer vs Calculator**

Computer
 * Stored Program computer —> Computer
 * Stores and Executes instructions    
   저장하고 명령을 실행하는 것

Calculator  
  * Fixed Program computer
  * Just calculate 

따라서 공학용 계산기는 COMPUTER

**1.2. Computer Science and Engineering** 

컴퓨터의 소프트웨어를 다루는 학문.
컴퓨터라는 물리적 기기를 연구하는 것이 아닌 Computer의 개념과 구조를 이해하고 구현하는 학문.

[!Alt 참고](Basic Computer Architecture.png)

* Program Counter-contains the address(location)of the instruction being executed at the current time
* ALU(Arithmetic Logic): +,-,*,/,And, Or, Not

**2. CPU and MicroProcessor**

**2.1.Architecture Naming** 

* x86
8080: 8bit
8086: 16bit
8088: 8bit
80286: 16bit
80386: 32bit

* IA64
Itanium: IA64 based 64bit, 1999

* AMD64
Opteron: x85-64basde 64bit, 2003
Athlon
AMD phenom
AMD FX
Ryzen 

* ~Intel 64~ == AMD64
Xeon: x 86-64 based 64 bit, 2004
Core 2
Core i Series

**2.2. CISC&RISC**

Complex Instruction Set Computer
- 복접한 명령구조
- 어드레싱에 강점
- Intel x 86, AMD64,...

Reduced Instruction Set Computer
- 명령어의 단순화
- 메모리 접근 횟수가 적음
- 저전력 프로세싱에 사용
- SPARC,ARM,...

**3. Memory**
컴퓨터에 사용할 수 있도록 정보를 저장하는 공간

* RAM(Random Access Memory)
  * 자유롭게 읽고 쓸 수 있는 주기억장치
  * 메모리 주소로 그 위치에 접근 
  * RAM의 어떤 위치로든 같은 시간에 접근(Random Access)
    Random Access: 한번에 들어가는 것, 바로 접근할 수 있는 것.
  * 컴퓨터가 느려지면 재부팅을 해야하는 이유

* ROM(Read Only Memory)
  * 전원이 공급되지 않아도 그 정보를 유지하는 주기억장치
  * 비싸거나 느려서 안정적인 정보를 저장해야 할 떄 사용.
  * BIOS, OS, FIRMWARE 정보 저장에 쓰임.
 
**4. OS(Operating System)**
시스템 하드웨어와 응용소프트웨어(한글, excel..)의 리소스를 관리하는 소프트웨어. 하드웨어와 응용프로그램사이에 명령을 전해주기 위한 것.

**4.1. Type**
 * Single-tasking/Multi-tasking
   * 한번에 1개/n개의 프로그램을 동시 수행
 * Single-user/Multi-user
 * Distribted 
   Hardware <--> OS <--> Application Software <--> Users
   
**4.2. Chrinicles of OS**

 * Unix 
   * Starting in the 1970s by AT&T
   * Ken Thompson, Denis Ritchie,..

 * Unix-like
   * Solaris
   * BSD
   * MacOS

 * Linux
   * Unix-clone OS
   * GNU/Linux
   * Sep 17 1991 by Linus Torvalds
   * Ubuntu
   * Fedora
   * CentOS
   * Debian
   * Linuc Mint
   * ...
 * Linux-like
   * Android
   * Tizen 
   * Chrome OS
   * ...
  
 * Windows 
   * CP/M-DOS --> MS-DOS
   * Windows1
   * ...
   * Windows 10
   * Windows 95
   * Windosw 98
   * Windows 2000

**5. Patch & Debug**

Patch: 만든 소프트웨어를 수정하는 과정
Debug: 오류를 제거하는 과정


**6. Computatinal Thinking**

정답이 정해지지 않음 문제에 대한 해답을 일반화 하는 과정 

**6.1.Process of Computational Thinking**

  1. 문제 조직화 (추상화): Problem Formulation
  2. 솔루션 구현 (자동화): Solution Expression
  3. 솔루션 실행 및 평가 (분석): Solution Execution & Evaluation
 
* 문제인지
  * 배가 고프다. 
* 문제 조직화
  * 문제 분해
    * 뭘 먹긴 해야겠다.
      * 집에서 해결함
      * 냉장고엔 뭐가있지? 밥은 해놨나? 라면을 끓여먹얼까?
    * 나가서 해결함
      * 편의점? 식당? 패스트푸드? 레스토랑?
* 패턴인지
  * 아! 배가 고프면 어디서 뭔가를 먹음으로써 Hunger가 False가 되는구나
* 일반화/추상화
  * 추상화(간결하고 명확하게 단순화, 일반화, 개념화)
    * 배가 고프면: {{어디}}에서 {{어떻게}} 해결함
  * 알고리즘 
* 솔루션 구현
* 솔루션 실행 및 평가
  * 솔루션대로 실행해서 나는 배고픔을 인지하고 해결하게 되었다.
  * 돈 보유량에 따라 다양한 선택지를 둬야겠다.
  * 집에서 밥이 없으면 굶지말고 밥을 해야겠다. 


