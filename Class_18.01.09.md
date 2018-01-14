18.01.09

**GOAL**
* 의사코드를 이해하고 본 코드를 작성하기 전 생각의 흐름을 의사코드로 구현한다.
* 알고리즘에 대해 이해할 수 있다.
* 자료구조에 대해 이해할 수 있다.

**1.Pseudocode**
Pseudocode == 의사코드
프로그램이나 알고리즘이 수행할 내용을 인간이 이해할 수 있는 언어로 표현하는 것. 프로그램을 설계할 때 *_밑그림 역할_.*

*fizzbuzz(Texh 면접 단골 질문)* 

    1부터 n까지 반복하면서,
    3의 배수는 "fizz"
    5의 배수는 "buzz"
    15의 배수는 "fizzbuzz"
    나머지는 숫자
    
	1.get integer from user ===> num, i == 1
	2. WHILE i is less than or equal to num
	3. if i is divisible by 3, print "fizz"
	4. if i is divisible by 5, print "buzz"
	5. if i is divisible by 15, print "fizzbuzz"
	6. else, pirnt i


*VAT Quize*

	제품 가격과 나라에 따른 다른 부가가치세를 계산해 그 가격을    
    보여주세요!
	
    * KR: 10%
    * JP: 8%
    * US: 주마다 다름
    * UK: 20%

	1. get price of item ==> item_price
	2. set tax rate (KR == 0.1, JP == 0.08,    
	   US == "depends on states" UK == 0.2)
    3. get contry_code (KR, JP, US, UK) 
    4. tax_rate is mached price with contry_code
    5. sales_tax is item_price times tax_rate
    6. total_price is item_price plus sales_tax


**2. Algorithm**
목표를 달성하거나 결과물을 생산하기 위해 필요한 과정들.

	1~100까지 더해봅시다!
    
    - 방법1
      1+2+3+...
      
    - 방법2
      1+100=101
      2+99=101
      ...
      101*50=5050
      
     -방법3
      n(n+1)/2
      
     문제를 해결하는 많은 방법들이 있지만 
     Algorithm is focus on **clarity!**
     
**2.1. Algorithm Conditions**
 * has external input
   외부로부터 어떤 입력이 있어야 한다.
 * has 1 or more result
   1개 이상의 결과가 나와야 한다.
 * clairity
 * finite trial
   한정되어야 한다.
 * simplicity
   단순해야한다.
 .
 . 
 . 
 
   
**Clarity** 
time complexity == **big O notation** 
자료의 수(n)이 증가할 때 시간의 증가 패턴을 나타낸 것.

**2.2. big O notation**
1
log n
n log n
n^2
n^3
2^n
n!

**2.3. Sort algorithms**
* O(n^2)
  * Bubble sort
  * Selection sort
  * Insertion sort
  
* O(n log n)
  * Merge sort
  * Heap sort
  * Quick sort---> 평균적으로 가장 빠른 방법
 
 
Quick sort: 피벗(중심값)을 기준으로 큰값 작은값을 나눈 뒤, 피벗을 옯겨 다시 수행하는 방법.


**3. Data Structure**
컴퓨터에서 데이터를 정리하는 효율적으로 사용할 수 있도록 정리하는 방법. 

**3.1. Data Structures in Web Development**
 * Binary Tree Search
   * Queue(BFS, Breadth First Search)
   * Stack(DFS,Depth First Search)
   
 Stack
 push: 넣은 순서대로 쌓는 것 
 pop: 위에서 부터 하나씩 빼내는 것
 LIFO(Last In First Out)
 
 Queue
 FIFO(First In First Out)
 
**4. Linked List**

**5. Tree**
순위 순서에 따른 모델.

[Alt]!(tree.jpg)

* root:2
* level:(0~3)
* child of 2: 7,5
* subtree: 6,5 11
* Node:(9)
* edge:(8)
