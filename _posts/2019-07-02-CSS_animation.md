---
layout: post
title: "CSS 애니메이션 4 - Animation"
subtitle: "@keyframes 규칙과 animation-duration, animation-delay 속성"
categories : CSS
tags: [CSS]
author: Nayeong Kim
comments: True
---

<div id='preview'>
CSS2에서는 애니메이션 효과를 주기 위해 자바스크립트 혹은 외부 플러그인을 사용해야만 했던 반면, CSS3에서는 animation속성을 사용하여 요소의 현재 스타일을 다른 스타일로 천천히 변화시킬 수 있게 되었다.
</div>


## Animation

CSS2에서는 애니메이션 효과를 주기 위해 자바스크립트 혹은 외부 플러그인을 사용해야만 했던 반면, CSS3에서는 animation속성을 사용하여 요소의 현재 스타일을 다른 스타일로 천천히 변화시킬 수 있게 되었다.

<br>

### 1. @keyframes 규칙과 animation-name 속성

CSS3에서 애니메이션 효과를 사용하기 위해서는 우선 애니메이션에 대한 키 프레임(keyframe)을 정의해야 한다.

`@keyframes` 에는 특정 시간에 해당 요소가 가져야할 CSS 스타일을 명시한다. 이렇게 스타일을 설정해 놓으면, 해당 요소의 스타일이 특정 시간까지 현재 스타일에서 명시한 스타일로 변화한다.

`animation-name` 속성은 해당 요소와 특정 키 프레임(keyframe)을 연결해주는 역할을 한다.

{% highlight scss %}
p{
	animation-name: moveLeft;
	animation-duration: 3s;
	-webkit-animation-name: moveLeft;
	-webkit-animation-duration: 3s;
}
@keyFrames moveLeft {
	from { margin-left:100%; }
	to { margin-left:0%; }
}
{% endhighlight %}

- `from` 키워드에는 처음 스타일을 명시하고, `to` 키워드에서는 마지막 스타일을 명시한다.
- 더 복잡한 애니메이션 효과를 주기 위해 from, to키워드 대신에 `퍼센트(%)` 키워드를 사용할 수 있다. 
  - 0%에는 처음 스타일을, 100%에는 마지막 스타일을 명시하고, 중간에 원하는 만큼의 프레임을 생성할 수 있다.

{% highlight scss %}
// p태그 글자 색상이 4초동안 무지개 색으로 변하는 애니메이션
p{
	animation-name: moveLeft;
	animation-duration: 4s;
	-webkit-animation-name: moveLeft;
	-webkit-animation-duration: 4s;
}
@keyFrames moveLeft {
	0% { color: red; }
	20% { color: orange; }
	40% { color: yellow; }
	60% { color: green; }
	80% { color: blue; }
	100% { color: purple; }
}
{% endhighlight %}

재생이 모두 끝나면 해당 요소는 맨 처음 가지고 있던 스타일로 되돌아간다. 위의 경우 빨간색으로 되돌아간다.

<br>

### 2. animation-duration 속성

- 애니메이션 효과를 재생할 시간을 설정한다.

- 재생 시간의 기본 값은 0초이므로, 재생할 시간을 명시하지 않으면 아무런 효과도 나타나지 않는다.

<br>

### 3. animation-delay 속성

애니메이션 효과가 나타나기까지 지연 시간을 설정한다. 즉, 애니메이션의 효과는 animation-delay 속성에 설정된 시간이 지난 뒤 나타난다.

{% highlight scss %}
// 2초뒤에 애니메이션이 실행되며, 애니메이션의 실행시간은 3초이다.
p{
	animation-name: moveLeft;
	animation-duration: 3s;
	animation-delay: 2s;
	-webkit-animation-name: moveLeft;
	-webkit-animation-duration: 3s;
	-webkit-animation-delay: 2s;
}
@keyFrames moveLeft {
	from { margin-left:100%; }
	to { margin-left:0%; }
}
{% endhighlight %}

<br>

### 4. animation-iteration-count 속성

- 애니메이션 효과의 **반복 횟수**를 설정한다. 
- 이 속성값으로 `infinite`를 설정하는 경우, 애니메이션의 효과가 무한히 반복된다.

{% highlight scss %}
// .once의 효과는 한번, .loop의 효과는 무한히 반복된다.
p{	
	animation-name: moveLeft;
	animation-duration: 4s;
	-webkit-animation-name: moveLeft;
	-webkit-animation-duration: 4s;
}
.once{
	animation-iteration-count: 1; 
	-webkit-animation-iteration-count: 1;
}
.loop{
	animation-iteration-count: infinite; 
	-webkit-animation-iteration-count: infinite;
}
@keyFrames moveLeft {
	0% { color: red; }
	20% { color: orange; }
	40% { color: yellow; }
	60% { color: green; }
	80% { color: blue; }
	100% { color: purple; }
}
{% endhighlight %}

<br>

### 5. animation-direction 속성

- 애니메이션의 진행방향을 결정한다.
- `reverse`, `alternate` 속성값으로 진행방향을 나타낸다.
  - `reverse` 는 반대방향. 즉, 애니메이션 방향이 `from` 에서 `to`로 진행된다.
  -  `alternate`  는 원래 진행방향

{% highlight scss %}
p{	
	animation-name: moveLeft;
	animation-duration: 4s;
	animation-direction: reverse;
	-webkit-animation-name: moveLeft;
	-webkit-animation-duration: 4s;
	-webkit-amimation-direction: reverse;
}
@keyFrames moveLeft {
	0% { color: red; }
	20% { color: orange; }
	40% { color: yellow; }
	60% { color: green; }
	80% { color: blue; }
	100% { color: purple; }
}
{% endhighlight %}

> `alternate` 속성값의 경우, 애니메이션이 반복될 때마다 방향을 계속해서 변경한다. 
>
> 즉, 애니메이션 효과가 from에서 to 방향으로 한 번 진행되고 나면, 다음번에는 to에서 from 방향으로 진행되게 변경된다. 때문에 효과를 여러번 반복할 때 `alternate` 을 사용하면 애니메이션이 더 자연스러워 보인다.
>

<br>

### 6. animation-timing-function 속성

애니메이션 효과의 시간당 속도를 설정한다.

- ease : 기본값, transition 효과가 천천히 시작되어, 빨라지다가 다시 느려진다.

- linear : transition 효과가 처음부터 끝까지 일정하게 진행된다.
- ease-in : transition 효과가 천천히 시작된다.
- ease-out : transition 효과가 천천히 끝난다.
- ease-in-out : 애니메이션 효과가 천천히 시작되어, 천천히 끝난다.
- cubic-bezier(n,n,n,n) : transition 효과가 사용자가 정의한 cubic-bezier 함수에 따라 진행된다.

<br>

### 7. animation 축약표현

모든 animation 속성을 이용한 스타일을 한 줄에 설정할 수 있다.

>animation: {-name} {-duration} {-timing-function} {-delay} {-iteration-count} {-direction}

**[ 축약 전 ]**

{% highlight scss %}
p{	
	animation-name: moveLeft;
	animation-duration: 4s;
	animation-timing-function: ease-in-out;
	animarion-delay: 2s;
	animation-iteration-count: 2;
	animation-direction: alternate;
}
{% endhighlight %}

**[ 축약 후 ]** 

{% highlight scss %}
p{	
	animation: moveLeft 4s ease-in-out 2s 2 alternate;
}
{% endhighlight %}


