---
title: "파이썬으로 배워보는 자료구조와 알고리즘 3 - 리스트(List)"
---

# 파이썬으로 배워보는 자료구조와 알고리즘 3
리스트(List)

{% include toc %}


- ## 리스트
  리스트는 선형 자료구조 중 가장 일반적인 자료구조이다. 배열과 연결 리스트로 나눌 수 있으며, 정렬되지 않은 경우 검색하는데 O(n)의 시간이 걸리는 단점을 가지고 있다. 정렬되어 있는 경우 배열의 경우 이진 탐색으로 O(log n)시간이 걸리지만, 연결리스트의 경우는 이진 탐색이 불가하다.

  리스트 자료구조의 동일한 특징은 아래와 같으며, 추상 자료형(ADT)으로 먼저 구현해보자.
  1. 데이터를 선형(Linear)으로 저장한다.
  2. 데이터를 추가/삭제/검색할 수 있다.
  3. 특정 인덱스의 데이터를 가지고 올 수 있다.
  4. 처음 혹은 마지막 데이터를 꺼내올 수 있는 기능이 있어야 한다.
  5. 리스트의 모든 데이터를 차례대로 출력할 수 있어야 한다. <br /><br />

  - 리스트의 추상 자료형(ADT) 혹은 메타 클래스
    ```python
    class BaseList:
      # 데이터의 추가
      def append(self, data):
          raise NotImplemented
      # 데이터의 탐색
      def search(self, data):
          raise NotImplemented
      # 데이터의 참조하기
      def get(self, index):
          raise NotImplemented
      # 데이터의 꺼내오기
      def pop(self):
          raise NotImplemented
      # 데이터의 삭제
      def remove(self, index):
          raise NotImplemented
      # 리스트 전체 출력
      def display(self):
          raise NotImplemented
    ```

- ## 배열(Array)
  - 메모리 상에 같은 타입의 자료가 연속적으로 저장된다. 정렬되어 있지 않다면, 탐색에 O(n)시간이 걸린다. 정렬되어 있다면, 이진 탐색으로 O(log n) 시간으로 줄일 수 있다. 하지만 정렬을 위해 삽입, 삭제하는데 배열을 한칸씩 밀거나 당기는데 오버헤드가 생긴다.

  - ArrayList 구현
    ```python
    class ArrayList(BaseList):
      def __init__(self):
          self.list = []
          self.count = 0

      def append(self, data):
          self.list.append(data)
          self.count += 1

      def search(self, data):
          return [index for index, stored in enumerate(self.list) if stored == data]

      def get(self, index):
          if 0 <= index < self.count:
              return self.list[index]
          else:
              raise IndexError

      def pop(self):
          val = self.list[self.count - 1]
          self.remove(self.count - 1)
          return val

      def remove(self, index):
          for _index in range(index, self.count - 1):
              self.list[_index] = self.list[_index + 1]

          del self.list[self.count - 1]
          self.count -= 1

      def display(self):
          for index in range(self.count):
              print(self.list[index])
    ```
  <br />


- ## 연결 리스트(Linked List)
  - 배열과 동일한 리스트 구조이지만, 연속된 메모리 공간을 사용하지는 않는다. 리스트는 노드를 단위로 저장되며, 하나의 노드는 데이터를 저장하는 공간과 다음 노드를 가르키는 참조값을 저장하는 공간으로 구성된다. 따라서 리스트 형태로 모든 노드가 연결되어 있는 구조이다.<br /><br />
  ![연결 리스트](https://upload.wikimedia.org/wikipedia/commons/3/37/Singly_linked_list.png) <br /><br />
  정렬되어 있지 않다면, 탐색하는데는 O(n)시간이 걸리고, 삽입에는 O(1), 삭제에는 O(n) 시간이 걸린다. 정렬되어야 한다면, 탐색하는데는 O(n)으로 동일하며, 삽입에는 O(n), 삭제에도 O(n)시간이 걸린다.


  - Linked List의 구현
    ```python
      class Node:
          def __init__(self, data, next):
              # 데이터를 저장한다.
              self.data = data
              # 다음 노드를 가르킴
              self.next = next


      class LinkedList(BaseList):
          def __init__(self, sort=None):
              self.head = Node(None, None)
              self.tail = None
              self.count = 0
              self.sort = sort if sort else lambda x, y: x > y

          def append(self, data):
              new_node = Node(data, self.head.next)
              self.head.next = new_node
              if not self.tail:
                  self.tail = new_node
              self.count += 1
              return new_node

          def append_with_sort(self, data):
              new_node = Node(data, None)
              prev = self.head
              while prev.next:
                  current = prev.next
                  if self.sort(current.data, data):
                      break
                  prev = prev.next

              new_node.next = prev.next
              prev.next = new_node

          def search(self, data):
              hits = []
              current = self.head
              while current.next:
                  current = current.next
                  if current.data == data:
                      hits.append(current)

              return hits

          def get(self, index):
              if 0 <= index < self.count:
                  current = self.head.next
                  for _index in range(self.count):
                      if _index == index:
                          return current
                      current = current.next
              else:
                  raise IndexError

          def pop(self):
              node = self.head.next
              self.head.next = node.next
              self.count -= 1
              return node

          def remove(self, index):
              before = None
              current = self.head.next
              for _index in range(self.count):
                  if _index == index:
                      if _index == 0:
                          self.head.next = current.next
                      else:
                          before.next = current.next

                  before = current
                  current = current.next
              self.count -= 1

          def display(self):
              current = self.head
              while current.next:
                  current = current.next
                  print(current.data)

    ```
  <br />
