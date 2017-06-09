---
title: "파이썬으로 배워보는 자료구조와 알고리즘 1 - 자료구조와 알고리즘의 정의, 복잡도"
---

# 파이썬으로 배워보는 자료구조와 알고리즘 1
자료구조와 알고리즘의 정의, 복잡도

{% include toc %}


- ## 자료구조
  자료구조는 데이터를 효율적으로 이용할 수 있도록 저장하는 방법이다. 이렇게 저장된 구조를 이용해 보다 효율적인 알고리즘을 사용할 수 있게 해준다. <br />

  대표적으로 데이터베이스에서 데이터를 효율적으로 관리하기 위해 저장되는 인덱스의 자료구조가 [B-트리](https://ko.wikipedia.org/wiki/B_%ED%8A%B8%EB%A6%AC)이다. <br />

  대부분의 Programming Languages에서는 이러한 자료구조를 각 언어의 특성에 맞게 효율적으로 구현해놓고 인터페이스를 제공해서 자료구조를 쉽게 사용할 수 있도록 도와준다. <br /><br />


- ## 자료구조의 분류
  - 구현에 따라
    - **배열(Array)** : 가장 일반적인 리스트 구조이다. 메모리 상에 같은 타입의 자료가 연속적으로 저장된다.
    - **연결 리스트(Linked List)** : 배열과 동일한 리스트 구조이지만, 연속된 메모리 공간을 사용하지는 않는다. 리스트는 노드를 단위로 저장되며, 하나의 노드는 데이터를 저장하는 공간과 다음 노드를 가르키는 참조값을 저장하는 공간으로 구성된다. 따라서 리스트 형태로 모든 노드가 연결되어 있는 구조이다.
    - **환형 연결 리스트(Circular Linked List)** : 연결 리스트로 모든 노드가 연결되어 있으며, 마지막 노드는 환형적으로 첫번째 노드를 가르킨다.
    - **이중 연결 리스트(Double Linked List)** : 단방향 연결 리스트는 노드는 다음 하나의 참조값만 저장할 수 있지만, 이중 연결 리스트에서는 이전/다음의 노드 모두를 저장한다. 따라서 연결된 두 노드는 서로를 가르키게 된다.
    - **해시 테이블(Hash Table)** : 각 개체가 해시값에 따라 인덱싱된다.

  - 형태에 따라
    - 선형(Linear) 자료 구조
      - **스택(Stack)** : 후입선출(Last-in First-out) 구조의 자료 구조이다. 데이터를 스택에 넣고 다시 꺼내면 역순이 된다.
      - **큐(Queue)** : 선입선출(First-in First-out) 구조의 자료 구조이다. 가장
      - **덱(Deque)** : 양쪽에서 넣고 뺄 수 있는 자료 구조이다. 스택과 큐가 합쳐진 구조라고 볼 수 있다.
    - 비선형(Non-Linear) 자료 구조
      - **트리(Tree)** : 부모 노드와 N개의 자식 노드로 구성된 자료 구조이며, 자식 노드도 재귀적으로 (서브)트리 형태로 구성된다.
        - **이진 트리(Binary Tree)** : 자식 노드는 오직 2개만 가지는 트리
        - **힙(Heap)** : 부모가 자식보다 항상 크거나 혹은 항상 작은 Rule을 가지는 이진 트리이다.
      - **그래프(Graph)** : 트리 구조와 비슷하지만, 순환 구조를 가진다. 즉, 어떤 노드를 시작으로 다시 시작한 노드로 돌아올 수 있다.


- ## 알고리즘
  알고리즘은 자료 구조에 저장되어 있는 데이터를 연산하여 어떠한 문제를 해결하기 위한 결과를 도출해내는 일련의 과정이다. <br />

  또한 아래의 조건을 만족해야 한다.
  1. 입력 : 제공되는 입력은 0개 이상이다.
  2. 출력 : 전달받은 입력에 대해서 의도하는 결과를 반환한다.
  3. 명확성 : 수행 과정은 명확하고 모호하지 않은 명령어로 구성되어야 한다.
  4. 유한성(종결성) : 유한 번의 명령어를 수행 후(유한 시간 내)에 종료한다.
  5. 효율성 : 모든 과정은 명백하게 실행 가능(검증 가능)한 것이어야 한다.


- ## 복잡도
  복잡도는 공간과 시간으로 나뉠 수 있다. 공간 복잡도는 알고리즘에 필요한 메모리 공간이 얼마인지, 시간 복잡도는 알고리즘이 동작하는 시간이 얼마인지 계산해내는 것이다. <br />
  메모리는 충분히 보충할 수 있지만, 시간은 추가할 수 없는 절대적인 가치를 가지고 있기 때문에 시간 복잡도를 더 우선시 한다.<br /><br />

  - 점근적 표기법(Asymptotic Notation)
    임의의 함수에 대하여 "함수의 입력값(정의역의 원소)이 커짐에 따라 그 출력값(그 원소의 상)이 얼마나 빠르게 커지는가"를 표현한다. <br />
    점근적 표기법 big-Θ 표기법, big-O 표기법, and big-Ω 표기법와 같이 3가지 표기법으로 나뉘지만, 주로 최악의 경우(Worst case)인 big-O를 사용한다. 왜냐면, 최선의 경우는 의미가 없으며, 평균적인 경우는 계산하기 어렵기 때문이다. <br />
    big-O는 T(n)으로 표현한 함수의 최고차항의 차수가 빅오가 된다.
    따라서, T(n) = 5n^3 + 8n^2 + 2n + 3 이면, O(n^3)으로 표기할 수 있는 것이다. <br /><br />

  - 시간 복잡도
    - O(1), O(log N), O(N), O(N log N), O(N^2), O(N!) 복잡도들을 그래프로 표현하면 다음과 같다.
    ![Time Complexity]({{ site.url }}/assets/images/{{ page.date | date: "%Y-%m-%d" }}/complexity.png)

    <br />

    - O(n)와 O(log n)을 비교하면 다음과 같다.

      | n | O(n)  | O(log n) |
      | -----  | -----  | ----- |
      | 500 | 500 | 9 |
      | 5,000 | 5,000 | 13 |
      | 50,000 | 50,000 | 16 |



- ## 시간 복잡도의 예
  - O(1)
  ```python
    # Sum 1 to n
    def sum(n):
      return n * (n + 1) / 2
  ```
  `Ex: Hash`
  <br />

  - O(lg n)
  ```python
    # Binary Search
    def search(self, node, data):
      if node is None:
          return None
      if node.data == data:
          return node

      if data < node.data:
          search(node.left, data)
      elif node.data < data:
          search(node.right, data)
  ```
  `Ex: Binary Search`
  <br />

  - O(n)
  ```python
    # Sequential Search from array
    def search(self, data):
      for index, stored in enumerate(list):
        if stored == data:
          return index
      return None
  ```
  `Ex: Sequential Search`
  <br />

  - O(n lg n)
  ```python
    # quick sort
    def quick_sort(array, start, end):
      if start >= end:
          return

      pivot = partition(array, start, end)
      quick_sort(array, start, pivot - 1)
      quick_sort(array, pivot + 1, end)

      return array
  ```
  `Ex: Quick sort, Merge Sort, Heap Sort`
  <br />

  - O(n^2)
  ```python
  # bubble sort
  def bubble_sort(nums):
  	for i in range(len(nums) - 1):
  		for j in range(0, len(nums) - 1 - i, 1):
  			if nums[j] > nums[j + 1]:
  				swap(nums, j, j + 1)

  	return nums
  ```
  `Ex: (Nested Loop) Bubble sort, Insertion sort, Selection sort`
  <br />
