---
layout: post
title: "원격지(Github)의 특정 디렉토리만 git clone 하기"
subtitle: "Sparse Checkout 활성화"
categories : Git
tags: Git
author: Nayeong Kim
comments : True
---

<div id='preview' class='display-none'>
github 블로그에 포스팅을 하려고 하는데, 개인 노트북이 아닌 공용 컴퓨터에서 해야하는 일이 생겼다.  
<br/>
이처럼 원격지의 모든 폴더와 파일을 로컬로 가져올 필요가 없는 경우, 특정 폴더만 클론하자.
</div>

## 특정 디렉토리만 clone하기

github 블로그에 포스팅을 하려고 하는데, 개인 노트북이 아닌 공용 컴퓨터에서 해야하는 일이 생겼다.  
이처럼 원격지의 모든 폴더와 파일을 로컬로 가져올 필요가 없는 경우, 특정 폴더만 클론하자.

<br/>

#### 원격 저장소의 폴더 구조
> 
> ├─assets
> <br/>
> │  ├─css
> <br/>
> │  ├─img
> <br/>
> │  └─js
> <br/>
> ├─_includes
> <br/>
> ├─_layouts
> <br/>
> ├─_posts
> <br/>
> └─_sass
> <br/>
>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ├─base
> <br/>
>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ├─external
> <br/>
>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ├─includes
> <br/>
>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; └─layouts
> 

포스팅을 하기 위해선 `_posts`폴더와 이미지를 저장할 `assets/img`폴더를 가져와야 한다.

<br/>

### 1. 로컬 저장소 만들기

{% highlight shell %}
# blog 폴더 생성 및 이동
$ mkdir blog && cd blog	
$ git init
{% endhighlight %}

<br/>

### 2.  remote 추가

f 옵션을 추가해야 현재 디렉토리의 master branch가 origin/master로 설정된다.
즉, f 옵션 없이 remote 디렉토리를 추가한다면 git pull origin master에서 origin/master를 찾을 수 없다는 에러가 뜰 것이다.
{% highlight shell %}
$ git remote add -f origin {원격 저장소 url}
{% endhighlight %}

<br/>

### 3. Sparse Checkout 활성화

{% highlight shell %}
# core.sparseCheckout true로 설정
$ git config core.sparseCheckout true
{% endhighlight %}

<br/>

### 4. spars-checkout파일에 checkout폴더 등록

{% highlight shell %}
# spars-checkout파일 생성 및 가져올 폴더명 등록
$ echo "{checkout하고 싶은 파일이나 디렉토리}" >> .git/info/sparse-checkout
{% endhighlight %}

<br/>

### 5. git pull

{% highlight shell %}
$ git pull origin master
{% endhighlight %}

<br/>

#### 최종 결과

`_posts`폴더와 `assets/img`폴더만 clone된 것을 확인할 수 있다.

> 
> ├─assets
> <br/>
> │  └─img
> <br/>
> └─_posts


