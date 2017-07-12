---
title: "파이썬으로 배워보는 자료구조와 알고리즘 4 - 스택(Stack)"
---

{% include toc %}


- ## 스택
  스택은 'LIFO; Last-in, First-out' 즉, 가장 마지막에 저장된 데이터가 가장 먼저 나오는 자료구조이다.
  예를 들어 동전탑을 높이 쌓는다고 생각해보자. 동전탑을 만들기 위해서는 이전에 쌓은 동전 위에 다음 동전을 올려야한다. 그리고 동전을 하나 꺼내려면 맨위에 있는 동전을 꺼내야한다. (중간의 동전을 꺼내려고 한다면 공든탑이 무너질 것임)
  따라서 제일 마지막에 쌓아올린 동전을 제일 먼저 꺼내게될 것이다. 이것이 바로 스택의 원리이다.
  <img width="300px" src="{{ site.url }}/assets/images/{{ page.date | date: "%Y-%m-%d" }}/coin_stack.jpg" />

  <br />

  스택에서 데이터를 저장하는 연산을 **Push**, 데이터를 빼내는 연산을 **Pop** 이라고 한다. 이러한 연산은 추후 다른 자료구조에서도 사용되니 기억해두면 좋다. 그림으로 보면 아래와 같다. <br />

  <img height="300px" src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/29/Data_stack.svg/600px-Data_stack.svg.png" />
  <br />

  스택 자료구조의 추상 자료형(ADT)으로 먼저 구현해보자. 이 ADT는 추후 큐에서도 동일하게 쓰인다.
  1. 데이터를 스택에 저장(Push)한다.
  2. 데이터를 스택에서 꺼내(Pop)낸다. 데이터를 Pop하고 나서는 스택에서 해당 데이터를 삭제된다.
  3. 데이터를 스택에서 꺼내전에 잠깐 참조(Peek)할 수 있다.
  4. 데이터가 비어 있다면(is_empty), Pop연산을 실행할 수 없다.
  5. 데이터가 꽉차 있다면(is_full), Push연산을 실행할 수 없다. (단, 저장할 데이터의 개수를 한정해야함)
  6. 스택에 있는 모든 데이터를 차례대로 출력할 수 있어야 한다. <br /><br />

  - 리스트의 추상 자료형(ADT) 혹은 메타 클래스
    ```python
      class BaseStackQueue:
        # 데이터의 추가
        def push(self, data):
            raise NotImplemented
        # 데이터의 꺼내오기
        def pop(self):
            raise NotImplemented
        # 데이터 참조하기
        def peek(self):
            raise NotImplemented
        # 비어있는지 확인
        def is_empty(self):
            raise NotImplemented
        # 꽉 차있는지 확인
        def is_full(self):
            raise NotImplemented
        # 리스트 전체 출력
        def display(self):
            raise NotImplemented
    ```

- ## 스택의 구현
  - 스택의 구현은 ArrayList나 LinkedList를 이용해 구현할 수 있다. 또한 python의 collection framework에는 deque(Double Ended Queue)만 구현되어 있어서 deque를 이용해서 스택으로 사용할 수도 있다.

  -  ArrayList(배열)로 구현
    ```python
      class ArrayStack(BaseStackQueue):
        def __init__(self, max_length=50):
          self.items = []
          self.top = 0  # top에는 데이터를 저장할 최신 위치를 가르킨다.
          self.max_length = max_length

        def push(self, data):
          if self.is_full():  # push할 수 있는지 확인
            raise Exception('스택이 꽉 찼습니다!')

          self.items.append(data)
          self.top += 1

        def pop(self):
          if self.is_empty(): # pop할 수 있는지 확인
            raise Exception('스택이 비었습니다!')

          self.top -= 1
          data = self.items[self.top]
          del self.items[self.top + 1]

          return data

        def peek(self):
          if self.is_empty():
            raise Exception('스택이 비었습니다!')

          return self.items[self.top - 1] # pop예정인 데이터를 참조한다.

        def is_empty(self):
          return self.top == 0  # top이 0이면, 저장된 데이터가 하나도 없는 것임

        def is_full(self):
          # top이 max_length와 동일하다는 것은 꽉 찬것임.
          return self.top == self.max_length

        def display(self):
          for index in range(self.top):
            print(self.items[index])
    ```
  <br />

  -  LinkedList(연결 리스트)로 구현
    ```python
      class ListStack(BaseStackQueue):
        def __init__(self,  max_length=50):
           self.head = Node()
           self.top = 0
           self.max_length = max_length

         def push(self, x):
           if self.is_full():  
            raise Exception('스택이 꽉 찼습니다!')
           self.head.next = Node(x, self.head.next) # head의 다음으로 노드를 삽입
           self.top += 1

         def pop(self):
           if self.is_empty():
             raise Exception('스택이 비었습니다!')

           data = self.peek()
           self.top -= 1
           self.head.next = self.head.next.next # head의 다음 노드를 삭제
           return data

         def peek(self):
           if self.is_empty():
             raise Exception('스택이 비었습니다!')

           return self.head.next

         def is_empty(self):
           return not self.top

         def is_full(self):
           return self.top == self.max_length

         def display(self):
           node = self.head.next
           while node:
               print(node.data)
               node = node.next
    ```
  <br />

  -  deque(in python collection framework)로 구현
    ```python
      # deque은 Double Ended Queue의 구현체이며, 양쪽에서 데이터를 넣거나 꺼낼 수 있다.
      # 하지만 Stack을 구현하기위해서는 한쪽에서만 넣고 한쪽에서 빼야한다.
      class Stack(deque):
        def push(self, x):  # push를 override 한다.
            super().appendleft(x)

        def pop(self):    # pop을 override 한다.
            super().popleft()

        def display(self):
          for node in self.__iter__():
              print(node)
    ```
