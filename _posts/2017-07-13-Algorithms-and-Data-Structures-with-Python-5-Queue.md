---
title: "파이썬으로 배워보는 자료구조와 알고리즘 5 - 큐(Queue)"
excerpt: "큐는 'FIFO; First-in, First-out' 즉, 가장 먼저 저장된 데이터가 가장 먼저 나오는 자료구조이다."
---

{% include toc %}


- ## 큐 (Queue)
  큐는 'FIFO; First-in, First-out' 즉, 가장 먼저 저장된 데이터가 가장 먼저 나오는 자료구조이다.
  예를 들면 음식점에서 줄을 서는 것이 바로 큐이다. 제일 먼저 줄을 선 사람이 먼저 서비스를 받게되는 것이다. <br />
  <img style="height:350px;" src="{{ site.url }}/assets/images/{{ page.date | date: "%Y-%m-%d" }}/line_queue.png" />


  <br />

  큐에서는 데이터를 저장하는 연산을 **Enqueue**, 데이터를 꺼내는 연산을 **Dequeue** 이라고 한다. 또한 **Enqueue** 와 **Dequeue** 의 방향을 위해 **Front** 와 **Rear**(아래에서는 Back)라는 참조 값이 필요하다. 그림으로 보면 아래와 같다. <br />
  <img style="height:350px;" src="https://upload.wikimedia.org/wikipedia/commons/5/52/Data_Queue.svg" />
  <br />

  큐 자료구조의 추상 자료형(ADT)으로 먼저 구현해보자. 이 ADT는 스택과 거의 동일하다.
  1. 데이터를 큐에 Rear방향으로 저장(Enqueue)한다.
  2. 데이터를 큐에서 Front방향으로 꺼내(Dequeue)낸다. 데이터를 Dequeue하고 나서는 큐에서 해당 데이터를 삭제된다.
  3. 데이터를 큐에서 꺼내전에 잠깐 참조(Peek)할 수 있다.
  4. 데이터가 비어 있다면(is_empty), Pop연산을 실행할 수 없다.
  5. 데이터가 꽉차 있다면(is_full), Push연산을 실행할 수 없다. (단, 저장할 데이터의 개수를 한정해야함)
  6. 큐에 있는 모든 데이터를 차례대로 출력할 수 있어야 한다. <br /><br />

  - 큐의 추상 자료형(ADT) 혹은 메타 클래스
    ```python
      class BaseQueue:
        # 데이터의 추가
        def enqueue(self, data):
            raise NotImplemented
        # 데이터의 꺼내오기
        def dequeue(self):
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

- ## 큐의 구현
  - 큐의 구현은 ArrayList나 LinkedList를 이용해 구현할 수 있다.
  ArrayList를 이용하는 경우 Circular Queue로 구현할 수 있다. Circular Queue로 구현하는 이유는 Queue 자료구조의 성격상 한쪽 방향으로 계속 움직이게된다. 위에서의 그림처럼 왼쪽에서 Enqueue하고 오른쪽에서 Dequeue하게되면, 저장 공간은 왼쪽 방향으로 계속 움직이게된다. 따라서 원형으로 구현하게 된다면, 방향성에 상관없이 효율적으로 공간을 활용할 수 있게되는 것이다.
  또한 Deque(Double Endded Quque; 덱이라고 발음)이라는 자료구조는 큐와 동일하지만 양쪽에서 데이터를 넣고 뺄 수 있다. python의 collection framework에는 deque이라는 클래스를 제공하기 때문에 이 클래스를 이용해서 Queue(혹은 Stack)를 구현할 수 있다. <br />
  <img width="500px" src="https://namu.wiki/w/%ED%8C%8C%EC%9D%BC:attachment/%ED%81%90(%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0)/deque.jpg" /> <br />

  -  ArrayList(배열)로 구현, Circular Queue로 구현
    ```python
      class ArrayQueue(BaseQueue):
        def __init__(self, max=MAX):
            self.max = max
            self.list = [None] * self.max
            self.size = self.front = self.rear = 0

        def is_empty(self):
            return self.size == 0

        def is_full(self):
            return self.next_idx(self.rear) == self.front

        def next_idx(self, idx):
            return (idx + 1) % self.max

        def enqueu(self, data):
            if self.is_full():
                raise Exception('큐가 꽉 찼습니다!')

            self.rear = self.next_idx(self.rear)
            self.list[self.rear] = data
            self.size += 1

        def dequeue(self):
            if self.is_empty():
                raise Exception('큐가 비었습니다!')

            self.front = self.next_idx(self.front)
            return self.list[self.front]

        def peek(self):
            return self.list[self.next_idx(self.front)]

        def display(self):
            current = self.front
            while current != self.rear:
                current = self.next_idx(current)
                print(self.list[current])
    ```
  <br />

  -  LinkedList(연결 리스트)로 구현
    ```python
      class ListQueue(BaseQueue):
        def __init__(self, max_length=50):
          self.front = None
          self.rear = None
          self.size = 0
          self.max_length = max_length

        def enqueue(self, data):
          if self.is_full():
            raise Exception('큐가 꽉 찼습니다!')

          new_node = Node(data)
          if self.is_empty():
            self.front = new_node
          else:
            self.rear.next = new_node              
          self.rear = new_node

          self.size += 1

        def dequeue(self):
          if self.is_empty():
            raise Exception('큐가 비었습니다!')

          del_node = self.front
          self.front = self.front.next
          self.size -= 1

          if self.is_empty():
            self.rear = None
          return del_node.data

        def peek(self):
          if self.is_empty():
            raise Exception('큐가 비었습니다!')

            return self.front

        def is_empty(self):
          return self.size == 0

        def is_full(self):
          return self.size == self.max_length

        def display(self):
          current = Node(None, self.front)
          while current.next:
            current = current.next
            print(current)
    ```
  <br />

  -  deque(in python collection framework)로 구현
    ```python
      # deque은 Double Ended Queue의 구현체이며, 양쪽에서 데이터를 넣거나 꺼낼 수 있다.
      # 큐를 구현하기위해서는 한 방향에서 넣고, 반대 방향에서 꺼내야한다.
      class Queue(deque):
        # push를 override 한다.
        def enqueue(self, x):  
            super().append(x) # 오른쪽에서 데이터를 enqueue 한다.

        def dequeue(self):
            super().popleft()  # 왼쪽에서 데이터를 dequeue 한다.

        def display(self):
          for node in self.__iter__():
              print(node)
    ```
