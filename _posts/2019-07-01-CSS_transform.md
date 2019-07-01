---
layout: post
title: "CSS 에니메이션 - 3D Transform"
subtitle: "CSS 에니메이션 효과 공부하기 2"
categories : CSS
tags: [CSS]
author: Nayeong Kim
comments: True
---

<div id='preview'>
CSS의 transform 속성을 사용하면 HTML 요소의 모양, 크기, 위치 등을 입체적으로 변화시킬 수 있다.
</div>



## 3D Transform

CSS의 transform 속성을 사용하면 HTML 요소의 모양, 크기, 위치 등을 입체적으로 변화시킬 수 있다. 

<br>

### 1. 3D Transform methods

3D Transform을 위해 제공되는 메서드는 아래와 같다.

<br>

#### a. rotate3d(): X, Y, Z축을 기준으로 회전

- rotateX, rotateY, rotateZ로 각각 사용 가능
- 해당 요소를 주어진 각도만큼 **X축, Y축, Z축을 기준으로 회전**시킨다.

{% highlight scss %}
// x축을 기준으로 20도만큼 회전
.rotate_X {
	transform: rotateX(20deg);
	-webkit-transform: rotateX(20deg);
	-ms-transform: rotateX(20deg);
 }

{% endhighlight %}

<br>

#### b. translate3d()  : 이동

- translateX, translateY, translateZ로 각각 사용 가능
- 현재 위치를 기준으로 해당 요소를 주어진 x축, y축, z축의 거리만큼 **이동**시킨다.

{% highlight scss %}
// x축으로 100px, y축으로 200px, z축으로 -100px
.trans_3d{
	transform: translate3d(100px, 200px, -100px);
	-webkit-transform: translate3d(100px, 200px, -100px);
	-ms-transform: translate3d(100px, 200px -100px);
 }

{% endhighlight %}

<br>

#### c. scale3d() : 크기 조절

- scaleX, scaleY, scaleZ로 각각 사용 가능
-  x축, y축, z축의 크기를 주어진 **배율만큼 늘이거나 줄인다.**

{% highlight scss %}
.scale_3d{
	transform: scale3d(20deg, 20deg, 20deg);
	-webkit-transform: scale3d(20deg, 20deg, 20deg);
	-ms-transform: scale3d(20deg, 20deg, 20deg);
 }

{% endhighlight %}

<br>

#### d. perspective() : 투영점, 원근감 표현

- https://webclub.tistory.com/486 를 참고했다.
- perspective는 3D원근감을 주는 초점이라고 할 수 있다.
- 이 속성으로 인해 3차원의 객체로 변환되어 실제와 같은 거리감을 갖게된다.
- 중요한 점은 3d속성으로 변형할 대상요소가 아닌 **해당 요소를 포함하고 있는 부모요소에 투영점을 설정**해야 한다.
- 부모요소에  perspective설정을 적용하는 경우, 개별 요소가 아닌 **각각의 자식 요소들이 원근감을 서로간에 영향을 미치면서 반영**된다.

> translateZ(300px)와 화면상에서 300px만큼 나와 떨어져 있음을 표현하고 싶다면, perspective 속성이 반드시 필요하다.

