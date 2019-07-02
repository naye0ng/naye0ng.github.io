---
layout: post
title: "CSS 애니메이션 1 - 2D Transform"
subtitle: "CSS 애니메이션 효과 공부하기 1"
categories : CSS
tags: [CSS]
author: Nayeong Kim
comments: True
---

<div id='preview'>
CSS의 transform 속성을 사용하면 HTML 요소의 모양, 크기, 위치 등을 자유롭게 변화시킬 수 있다.
</div>



## 2D Transform

CSS의 `transform` 속성을 사용하면 HTML 요소의 모양, 크기, 위치 등을 자유롭게 변화시킬 수 있다. 또한, HTML 객체를 움직이게 하거나 회전, 크기 및 각도를 한 번에 선언할 수 있다.

<br>

### 1. CSS 좌표 체계

![CSS좌표]({{ site.baseurl }}/assets/post/20190627/css.png)

CSS의 좌표 체계에서의 기준점은 브라우저의 왼쪽 상단이 된다.

그림에서 알 수 있듯, z축을 제공하므로 3D transform도 가능하다는 것을 알 수 있다.

<br>

### 2. 2D Transform methods

2D Transform을 위해 제공되는 메서드는 아래와 같다.

<br>

#### a. translate() : 위치 변경

- 원래 모습을 기준으로 현재 위치에서 해당 요소를 주어진 x축와 y축의 거리만큼 이동시킨다.

- 양수, 음수 모두 사용이 가능하다.

{% highlight scss %}
// x축으로 100px, y축으로 50px만큼 이동
.trans {
	transform: translate(100px, 50px);		
	-webkit-transform: translate(100px, 50px);
	-ms-transform: translate(100px, 50px);
 }

{% endhighlight %}

<br>

#### b. rotate() : 각도 변경

- 원래 모습을 기준으로 해당 요소를 주어진 각도만큼 시계방향으로 회전시킨다.
- 양수 : 시계방향, 음수 : 반시계방향으로 회전

{% highlight scss %}
// 시계방향으로 30도 회전
.rotate{
	transform : rotate(30deg);
	-wekit-transform : rotate(30deg);
	-ms-transform : rotate(30deg);
}
{% endhighlight %}

<br>

#### c. scale() : 크기 변경

- 주어진 배율만큼 늘리거나 줄인다.
- scale(너비, 높이)

{% highlight scss %}
// 너비는 1.5배 증가, 높이는 0.5배 감소
.scale{
	transform : scale(1.5, 0.5);
	-wekit-transform : scale(1.5, 0.5);
	-ms-transform : scale(1.5, 0.5);
}
{% endhighlight %}

<br>

#### d. skew() : 기울기 조절

- 주어진 각도만큼 x축 방향으로 기울인다.
- 양수이면 x축의 양의 방향으로, 음수이면 x축의 방향으로 기울기가 조절된다.

{% highlight scss %}
// x축으로 30도 기울기 
.skew{
	transform : skewX(20deg);
	-wekit-transform : skewX(20deg);
	-ms-transform : skewX(20deg);
}
{% endhighlight %}

<br>

#### e. matrix()

matrix 메소드는 모든 2D transform 메소드를 한 줄에 설정할 수 있도록 한다.

> **matrix 메소드의 메개변수 순서**
>
> matrix(scaleX(), skewY(), skewX(), scaleY(), translateX(), translateY())

{% highlight scss %}
// 너비 2배, y축으로 기울기 30, x축으로 기울기 20, x축으로 150px, y축으로 100px 이동
.matrix{
	transform : matrix(2, 0.3, 0.2, 1.3, 150, 100);
	-wekit-transform : matrix(2, 0.3, 0.2, 1.3, 150, 100);
	-ms-transform : matrix(2, 0.3, 0.2, 1.3, 150, 100);
}
{% endhighlight %}



