---
layout: single
title: "[자료구조] 자료구조 기초"
categories: 자료구조
tag: [자료구조, data structure, stack, queue]

---

### 자료구조

자료구조란 여러 데이터들의 묶음을 저장하고, 사용하는 방법을 정의한 것이다.

데이터는 정해진 규칙없이 저장하거나, 하나의 구조로만 정리하고 활용하는 것보다 **데이터를 체계적으로 정리하여 저장해두는게 데이터를 활용하는 데 있어  훨씬 유리하다.**

<center>

<img src="../../images/2022-07-22-datastructure_first/image-20220721224557980.png" alt="image-20220721224557980" style="zoom: 44%;" />

</center><br>

가장 많이 쓰이고 알고리즘 테스트에 자주 등장하는 네가지

- Stack
- Queue
- Tree
- Graph


**Stack**

Stack은 데이터를 순서대로 쌓는 자료구조이다.  
자료구조 Stack의 특징은 입력과 출력이 하나의 방향으로 이루어지는 제한적 접근에 있으며 이런 Stack자료구조의 정책을 LIFO(Last In First Out) 혹은 FILE(First In Last Out)이라고 부르기도 한다.  
Stack에 데이터를 넣는 것을 PUSH, 데이터를 꺼내는 것을 POP이라고 한다.

**Queue**

자료구조 Queue는 Stack과 반대되는 개념으로 먼저 들어간 데이터가 먼저나오는 FIFO(First In First Out) 혹은 LILO(Last In Last Out)을 특징으로 갖고 있다.  
Queue에 데이터를 넣는 것을 enqueue, 데이터를 꺼내는 것을 dequeue라고 한다.  
자료 구조 Queue는 데이터가 입력된 순서대로 처리할 때 주로 사용한다.