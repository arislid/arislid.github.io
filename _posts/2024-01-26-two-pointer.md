---
layout: single
title: "Two Pointer"
tags: Algorithm
date: 2024-01-26
categories: Algorithm
toc: "true"
toc_sticky: "true"
toc_label: 목차
Keywords: [Algorithm, Two Pointer]
---
- [x] 최초 작성일자: 2023-05-10
- [x] 업로드 일자: 2024-01-26


# 투 포인터 알고리즘
투 포인터 알고리즘은 배열이나 리스트와 같은 선형 자료구조에서 2개의 포인터를 사용하여 문제를 효율적으로 해결하는 기법입니다. 이 알고리즘은 주로 정렬된 배열이나 리스트에서 특정 조건을 만족하는 원소를 찾거나, 배열의 연속된 부분 집합 중에서 특정 조건을 만족하는 경우를 찾을 때 사용됩니다. 투 포인터 알고리즘은 시간 복잡도와 공간 복잡도를 줄이는 데 도움을 줍니다.

투 포인터 알고리즘은 두 개의 포인터가 서로 다른 속도로 움직이며 해결하는 것입니다. 시작점과 끝점으로 설정해서 서로 다른 포인터가 만날 때까지 반복해서 움직이거나 느린점과 빠른점이 같은 방향에서 시작하되 서로 다른 속도로 이동해서 둘 다 끝에 다다를 때까지 반복한다.

## 언제 투 포인터를 사용하나?
1. 두 수의 합이 목표로 정한 값과 같은 수를 찾을 때
2. 링크드 리스트에서 반복을 찾을 때
3. 링크드 리스트에서 중간점을 찾을 때
4. 링크드 리스트나 배열에서 역전할 때
5. 특정 조건을 만족하는 연속적인 하위 배열을 유지하면서 슬라이딩 윈도우 문제를 해결할 때

## 복잡도
단순한 나열에서 한 포인터의 인덱싱만으로 문제를 해결할 때는 $O(n^2)$가 될 수도 있어 시간이 오래 걸리는 경우가 많지만, 투 포인터를 사용하면 $O(n)$가 되어 데이터 수가 많을 때 좋은 전략으로 사용할 수도 있다.

[//]: #### (생각)그렇다면 EDA할 때 Two Pointer를 써서 분석해볼까...?%%

# 투 포인터 vs 슬라이딩 윈도우
둘다 2개의 포인터(여기서는 인덱스라고 하겠다)를 활용하여 문제 해결하는 알고리즘인 것은 동일하나, 투 포인터는 인덱스 위치가 특정 규칙없이 조건에 따라 움직일 때 사용된다면, 슬라이딩 윈도우는 두 인덱스 사이의 크기가 고정적이라 일정한 간격으로 움직여야 한다는 점에서 차이점이 있다.

![two-pointer-vs-sliding-window](\assets\images\Pasted image 20230510222258.png)

[출처](https://velog.io/@hysong/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%ED%88%AC-%ED%8F%AC%EC%9D%B8%ED%84%B0-vs-%EC%8A%AC%EB%9D%BC%EC%9D%B4%EB%94%A9-%EC%9C%88%EB%8F%84%EC%9A%B0)

|이름|정렬 여부|윈도우 사이즈|이동 방향|
|---|---|---|---|
|투 포인터|대부분 O|가변|→ ←|
|슬라이딩 윈도우|X|불변|→|


# 파이썬 예시
## 1. 같은 방향에서 시작하는 투 포인터
```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def find_middle(head):
    slow = head
    fast = head

    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

    return slow

# Example usage:
# Creating a linked list with elements 1, 2, 3, 4, 5
head = ListNode(1, ListNode(2, ListNode(3, ListNode(4, ListNode(5)))))
middle = find_middle(head)
print("Middle element:", middle.val)  # Output: Middle element: 3

```

## 2. 다른 방향에서 시작하는 포인터
```python
def is_palindrome(s):
    left, right = 0, len(s) - 1

    while left < right:
        if s[left] != s[right]:
            return False
        left += 1
        right -= 1

    return True

# Example usage:
s1 = "racecar"
s2 = "hello"
print("Is '{}' a palindrome? {}".format(s1, is_palindrome(s1)))  # Output: Is 'racecar' a palindrome? True
print("Is '{}' a palindrome? {}".format(s2, is_palindrome(s2)))  # Output: Is 'hello' a palindrome? False

```


[//]: # C++ 예시%%