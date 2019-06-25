---
layout: post
title: "클러스터링(Clustering)"
categories : Bigdata
tags: [Bigdata]
author: Nayeong Kim
comments: True
---

<div id='preview'>
클러스터링이란 간단하게 데이터의 유사도에 의해 k개의 그룹으로 나눈 것을 말하며, 주로 추천시스템에 사용된다.
</div>


## 클러스터링(Clustering)

클러스터링이란 간단하게 데이터의 유사도에 의해 k개의 그룹으로 나눈 것을 말하며, 주로 추천시스템에 사용된다.

<br>

### 1. Clustering Algorithm

#### a. K-means Clustering

1. 랜덤하게 Clustering한 후, 평균점(center = means)을 계산한다.
2. 각 포인트가 어느 평균점에 더 가까운가를 파악하여 다시 Clustering을 진행한다.
3. 과정1, 2를 반복한다.
   - 이때, 포인터들이 속한 그룹에 변화가 없다면 멈추게 된다.

*처음 랜덤값에 의해 찾아지는 클러스터링의 결과가 달라질 수 있으므로, 이 과정을 여러번 진행한다.*

**[ 단점 ]**

- 클러스트의 사이즈가 크거나 작은 경우 잘 찾지 못함
- 평균점으로 부터 원의 띄는 모양만을 찾아내는 경향이 있다.
- 클러스터에서 아주 먼 곳에 있는 점이 존재하는 경우, 이 점 하나로 인해 평균점이 실제 데이터들가 존재하지 않는 곳을 가리키게 된다. 

이러한 단점을 해결하기 위해 `K-Medoids` 알고리즘을 사용한다.

<br>

#### b. K-medoids

`K-means Clustering`과 비슷하지만, 평균점은 실제 존재하는 데이터를 평균점으로 선택하는 알고리즘이다. 이 경우 아웃라인에 포인터가 있더라도 포인터가 몰려있는 곳의 점이 평균점으로 선택되므로 비교적 안정적이다.

<br>

#### c. Hierarchical Clustering

**[ Bottom-up 방식 ]**

- 모든 포인트가 하나의 독립적인 클러스터라고 가정.
- 모든 n개의 포인트들의 쌍의 거리를 계산하여 제일 가까운 쌍들을 하나의 클러스트로 머지함으로써 클러스트의 개수를 하나씩 줄이면서 전체 클러스터의 개수가 k개가 되면 종료하는 방식이다.

> 두 클러스트 간의 거리를 계산하는 방법에 따라 성능의 차이가 생길 수 있다.
>
> ![supervised Learning]({{ site.baseurl }}/assets/post/20190625/1.png)
>
> - Single-link : 두 클러스터 내의 모든 쌍들의 거리 중 최소 값
> - Complete-link : 두 클러스터 내의 모든 쌍들의 거리 중 최대 값
> - Average-link : 모든 쌍들의 거리의 평균
> - Centroid-link : 두 클러스트의 평균점 사이의 거리

<br>

#### d. DBSCAN Clustering

>**선행 지식**
>
>- Eps : maximum radius of the neighborhood
>- MinPts : Minimum number of points in an Eps-neighborhood of that point, Eps-neighborhood를 구성하는 최소 포인트의 개수
>- Neps(p) : {q belongs to D &#124; dist(p,q) <= Eps}, 점 p로부터의 거리가 Eps 보다 작은 점 q들의 집합
>- Core point 
> - p is a core point if &#124;Neps(q)&#124; >= MinPts, q의 Neps의 개수가 MinPts보다 많다면 core point
> - otherwise, p is border point
>- Directly density-reachable : (한번에)MinPts를 만족하는 Neps(p) = {q,…} 인 경우, q는 p로부터 directly density-reachable이다.
>- Density-reachable : 몇 번에 걸쳐라도 MinPts를 따져서 p부터 q를 찾아가는 경우
>- Density-connected : 어떤 점 o에 대하여 p와 q모두 density-reachable하다면, p와 q는 density-connected하다고 할 수 있다.
>
>1. 아래의 조건을 만족한다면, D의 포인트들에 대하여 클러스터 C는 Density-based cluster
>   - For every Pi, Pj in D, if Pi in C and Pj is Density-reachable form Pi, Pj belongs to C
>   - For every Pi, Pj in C, Pi is Density-reachable form Pj
>2. Outlier
>   - if a point p is border point and does not belongs the any other cluster, p is outer


![supervised Learning]({{ site.baseurl }}/assets/post/20190625/2.png)

어떤 포인터(in unvisited)를 기준으로 Eps를 radius로하는 원을 그려 MinPts를 만족하는 클러스트를 찾아낸다.

*` DBSCAN`는 `Hierarchical `와 달리, 클러스터의 개수 K를 정할 필요가 없다. Eps, MinPts를 통해 클러스트가 조절된다.*









