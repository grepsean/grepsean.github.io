---
title: "파이썬으로 배워보는 자료구조와 알고리즘 2 - 재귀(Recursion)"
---

# 파이썬으로 배워보는 자료구조와 알고리즘 2
재귀(Recursion)

{% include toc %}


- ## 재귀함수
  자기 자신을 재귀적으로 호출하는 함수이다. 아래 그림처럼 화면 녹화할때 녹화되는 창을 띄우면 재귀적으로 녹화되는 화면이 무한하게 표현되는 것을 볼 수 있다.
  ![화면녹화](https://upload.wikimedia.org/wikipedia/commons/b/b3/Screenshot_Recursion_via_vlc.png) <br />

- ## 재귀 함수의 특징
  재귀 함수는 논리적으로 자기 자신을 호출하는 것이지만, 실제 메모리상으로는 Code영역에 있는 함수가 Stack 영역으로 추가(복사)가 되면서, 마치 자신과 동일한 동작을 하는 다른 함수가 실행되는 것처럼 보일 수 있다. <br />

  모든 재귀 함수는 Iterable하게 Loop로 표현할 수 있다. 반대로 모든 Iterable한 Loop도 재귀적으로 표현할 수 있다.

- ## Factorial 함수
  가장 대표적인 재귀로 표현 가능한 함수이다. 1부터 N까지의 곱을 누적해나가는 함수이다. <br />

  재귀 문제를 풀기위해서는 재귀적인 사고가 필요하는데, 이는 분할 정복([Divide and conquer](https://ko.wikipedia.org/wiki/%EB%B6%84%ED%95%A0_%EC%A0%95%EB%B3%B5_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)) 방법과 일치한다. 큰 문제를 작은 문제로 쪼개서 점진적으로 문제를 풀어나가는 방식이다. <br />

  이것을 Factorial 문제에 적용해보자. 입력된 n에 대한 Factorial은 n-1까지의 Factorial 한 결과에 n을 곱한 것이고, n-1에 대한 Factorial은 n-2까지의 Factorial에 n-1을 곱한 것이 될 것이다. 이렇게 무한히 반복되게 될 것이다.  <br />

  하지만 이런 재귀적 접근에는 한가지 함정이 있다. 바로 무한히 재귀적으로 반복된다는 것이다. 따라서 재귀적 반복을 빠져나올 수 있는 하나 이상의 필수이다.
  Factorial에서는 n=1일때는 값이 1로 정해져 있다. 이것이 바로 탈출 조건(Base case)이 되는 것이다. <br />
  <!-- TODO : 그림 설명 필요 -->

  - Factorial의 구현
  ```python
    def factorial(n):
      if n == 0:
          #탈출 조건(Base case)
          return 1
      else:
          # 재귀적으로 자기 자신의 함수를 호출해주고 있다.
          return factorial(n - 1) * n
  ```

- ## Fibonacci 수열
  Fibonacci 수열은 이전 두개의 값을 합해서 그 다음 수를 만들어나가는 수열이다.
  이것도 재귀적 사고를 적용해보자. 입력 n에 대해서 결과를 구하려면 n-1값과 n-2을 합한 값이 될 것이다. n-1값을 구하기 위해서는 n-2값과 n-3값을 합해야하며.. 이런 것이 무한히 반복된다.
  또한 탈출 조건(Base case)는 n=1일때는 0이고, n=2일때는 1로 정해져 있다. <br />
  - Fibonacci의 구현
  ```python
    def fibonacci(n):
      if n <= 1:
          #탈출 조건(Base case) 1
          return 0
      elif n == 2:
          #탈출 조건(Base case) 2
          return 1
      else:
          # 재귀 호출을 두번이나 한다.
          return fibonacci(n - 2) + fibonacci(n - 1)
  ```
  <br />

- ## Hanoi 타워
  하노이 타워 문제는 재귀의 끝판왕이라 불릴만큼 재귀적 사고를 적용할 수 있는 최고의 퍼즐이다. <br />
  ![하노이타워](https://upload.wikimedia.org/wikipedia/commons/6/60/Tower_of_Hanoi_4.gif)

  총 3개의 기둥이 있고 첫번째 기둥에 작은 원판이 위에 있도록 순서대로 쌓여져 있다. 첫번째 기둥이 있는 원판들을 마지막 기둥으로 옮겨야하며 최종적으로 동일한 순서를 유지해야 한다. 이때 다음 두 가지 조건을 만족시켜야 한다.
    1. 한 번에 하나의 원판만 옮길 수 있다.
    2. 큰 원판이 작은 원판 위에 있어서는 안 된다.





  하노이 타워 문제에도 재귀적 사고를 적용해보자.
  1. 일단 n번째 즉 제일 마지막 원판이 마지막 기둥 제일 아래에 위치시켜야 한다. 이것을 위해서는 n-1개의 원판은 중간 기둥에 모두 옮겨져 있어야 한다.
  2. 중간 기둥에 있는 n-1개의 원판중 n-1번째 원판을 마지막 기둥으로 옮겨야한다. 이것을 위해서는 n-2개의 원판을 비어있는 첫번째 원판으로 옮겨야한다.
  3. ...이런 반복이 무한하게 반복된다.
  여기서 각 단계 마다의 탈출 조건(Base case)은 옮겨야할 원판이 아무것도 없다면 종료될 것이다.

  - Tower of Hanoi의 구현
    ```python
    def hanoi(n, start, waypoint, destination):
      if n == 0:
          # 탈출 조건
          return
      # 크게 두번 옮긴다.
      # 1. 일단 n-1까지를 출발 기둥(Start)에서 중간 기둥(Waypoint)을 거쳐 도착 기동(Destination)으로 옮긴다.
      hanoi(n - 1, start, destination, waypoint)
      # 2. 그리고 출발 기둥(Start)에 남아있는 n번째(제일 큰) 원판을 도착 기동(Destination)기둥으로 바로 옯긴다.
      print('{} move {} => {}'.format(n, start, destination))
      # 3. 중간 기둥(Waypoint)에 남아있는 n-1까지들을 다시 출발 기둥(Start)를 겨처 도착 기동(Destination)으로 옮긴다.
      hanoi(n - 1, waypoint, start, destination)
    ```
  <br />
