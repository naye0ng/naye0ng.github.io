---
layout: post
title: "CSS 애니메이션 3 - Transition"
subtitle: "CSS 애니메이션 효과 공부하기 3"
categories : CSS
tags: [CSS]
author: Nayeong Kim
comments: True
---

<div id='preview'>
CSS에서는 transition속성을 통해 정해진 시간동안 요소의 속성값을 부드럽게 변화시킬 수 있다.
</div>



## 1. 2D Transition

CSS에서는 transition속성을 통해 정해진 시간동안 요소의 속성값을 부드럽게 변화시킬 수 있다.

<br>

transition 속성은 아래와 같이 정의된다.

1. 해당 요소를 변화시킬 transition 효과를 설정한다.
2. transition 효과가 지속될 시간을 설정한다.
   - 지속 시간의 기본 값은 0으로, 효과의 지속시간을 명시하지 않는 경우 아무런 효과도 나타나지 않는다.

<br>

### a. transition-timing-function

transition 효과의 시간당 속도를 설정한다.

- ease : 기본값, transition 효과가 천천히 시작되어, 빨라지다가 다시 느려진다.
- linear : transition 효과가 처음부터 끝까지 일정하게 진행된다.
- ease-in : transition 효과가 천천히 시작된다.
- ease-out : transition 효과가 천천히 끝난다.
- ease-in-out : 애니메이션 효과가 천천히 시작되어, 천천히 끝난다.
- cubic-bezier(n,n,n,n) : transition 효과가 사용자가 정의한 cubic-bezier 함수에 따라 진행된다.



> cubic-bezier란? transition 효과를 처음부터 끝까지 제어하는데 사용된다.

<br>

### b. transition-delay

transition 효과가 나타기기 전까지의 지연 시간을 설정한다. 즉, transition 효과는 delay로 지정된 시간이 흐른 뒤에야 비로소 시작된다.

<br>

## 2. transition(전환)-transform(변형)

transition(전환)과 transform(변형)을 같이 사용함으로써 간단한 애니메이션을 구현할 수 있다.









