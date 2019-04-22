---
layout: post
title: "[알고리즘] 서로소 집합(Disjoint Set)"
subtitle: "Python으로 서로소 집합 만들기"
author: Nayeong Kim
tags: [Algorithm, Python]
comments : True
---

# 서로소 집합(Disjoint Set)

## 1. 상호배타 집합

서로소 또는 상호배타 집합들은 **서로 중복되는 원소가 없는 집합**들이다. 즉, 교집합이 없다.

집합에 속한 하나의 특정 멤버를 통해 각 집합들을 구분한다. 이를 대표자(representative)라고 한다.



## 2. 상호배타 집합 표현

상호배타 집합을 표현하는 방법 : 연결 리스트, 트리

상호배타 집합의 연산 : makeSet(), findSet(), union()

### 2-1. 연결리스트

- 같은 집합의 원소들은 하나의 연결리스트로 관리한다.
- 연결리스트의 맨 앞의 원소를 집합의 대표 원소로 삼는다.
- 각 원소는 집합의 대표원소를 가리키는 링크를 갖는다.



### 2-2. 트리

- 하나의 집합을 하나의 트리로 표현한다.
- 자식 노드가 부모 노드를 가리키며, 루트 노드가 대표자가 된다.
- makeSet() 연산에서 둘다 representative라면 둘 중에 하나를 representative로 삼는다.
- union()연산에서는 부모(representative)끼리 연결한다.

[연산의 효율을 높이기]

- Path compression : 

  - findSet()을 행하는 과정에서 만나는 모든 노드들의 부모를 representative로 연결하여 트리의 높이를 감소시킨다.

- Rank를 이용한 Union : 

  - 각 노드는 자신을 루트로 하는 subtree의 높이를 Rank라는 이름으로 저장한다. 
  - 두 집합을 합칠때 rank가 낮은 집합을 rank가 높은 집합에 붙인다.(rank가 낮은 집합에 높은 집합을 붙이는 경우, 전체 rank가 증가하게 된다.)
