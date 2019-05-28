---
layout: post
title: "Jekyll과 Github Page로 블로그 만들기(1)"
subtitle: "rbenv환경에서 Jekyll 블로그 설치"
author: Nayeong Kim
categories : Jekyll
tags: [GitHub, Jekyll]
comments : True
---

git을 이용해 commit과 push로 간단하게 블로그에 글을 쓸 수 있고, 로컬에서 블로그를 관리할 수 있다는 장점 때문에 Jekyll과 Github Page를 사용하여 블로그를 만들었다.

## Jekyll과 Github Page

`Jekyll`은 markdown으로 작성된 문서를 HTML파일로 변환해주는 역할을 한다. 즉, 로컬에서 `Jekyll`을 설치하면 간단하게 웹 페이지를 만들 수 있다. 하지만 로컬에서 블로그를 돌리려면 컴퓨터 전원을 항상 켜둬야 하며 외부접속을 위해 공유기의 포트 문제도 해결해야 한다. 이 문제를 해결하기 위해 `GitHub Page`를 사용한다. 

`GitHub Page`는 GitHub에서 제공하는 정적 웹사이트 호스팅 서비스이다. 정적 페이지이므로 서버가 필요한 백엔드 부분(Database)은 사용할 수 없으며, 프론트 부분(HTML, CSS, Javascript)만 동작한다.

`Jekyll`과 `GitHub Page`를 사용하면, 로컬에서 `Jekyll`을 사용해 블로그를 생성 및 테스트하고 GitHub에 소스파일을 push하여 쉽고 간단하게 웹 사이트를 만들 수 있다.

<br>

## 로컬에 Jekyll 환경 구축하기

`Jekyll`은 `GitHub Page`의 내부 엔진으로 Github에 markdown파일을 업로드 하면, `GitHub Page`가 해당 파일을 HTML로 변환하여 호스팅을 해준다. 그렇다면, '로컬에 굳이 Jekyll을 설치할 필요가 있을까?'라는 생각을 할 수 있다. 하지만 Github에 파일을 올린 후 해당 내용이 변환되어 반영되기까지 생각보다 시간이 오래걸리기 때문에 로컬환경에서 테스트를 마친 후에 commit하는 것이 좋다.

<br>

### 1. Jekyll 설치 환경 만들기

Jekyll은 Ruby로 만들어졌기에 로컬환경에서 Jekyll을 사용하기 휘해서는 Ruby가 필요하다. 맥북에는 기본적으로 Ruby가 설치되어 있지만, 버전이 낮아서 바로 Jekyll을 사용할 수 없다. 때문에 Ruby버전을 업그레이드하거나 버전관리도구를 사용해야한다. 그래서 필자는 Ruby의 버전관리도구인 rbenv를 설치해서 사용하였다.

<br>

#### 1-1. rbenv 설치

{% highlight shell %}

$brew install rbenv ruby-build

{% endhighlight %}

<br>

#### 1-2. rbenv 설정 추가

사용자의 홈 디렉토리에 있는 .bash_progile에 rbenv에 대한 설정을 추가해야한다. vi나 nano에디터를 사용하여 .bash_profile을 열어 아래 내용을 추가한다.

{% highlight shell %}

# nano에디터로 홈 디렉토리에서 .bash_profile 열기
$nano ~/.bash_profile

{% endhighlight %}

아래 내용을 복사사여 저장한 후, 쉘을 종료하고 새로 열어준다.

{% highlight shell %}

# rbenv 설정
export PATH="$HOME/.rbenv/bin:$PATH"
eval "$(rbenv init -)"

{% endhighlight %}

<br>

#### 1-3. ruby 설치 및 버전 지정

{% highlight shell %}

$rbenv install 2.5.3
$rbenv global 2.5.3

# ruby 설치 버전 적용
$rbenv rehash

{% endhighlight %}

<br>

### 2. Jekyll 설치

{% highlight shell %}

$gem install jekyll bundler github-pages

{% endhighlight %}

<br>

### 3.Jekyll 블로그 생성 및 실행

#### 3-1. Jekyll 블로그 생성

{% highlight shell %}

$jekyll new {블로그 이름}
$cd {블로그 이름}

{% endhighlight %}

<br>

#### 3-2. bundle로 패키지 업데이트

{% highlight shell %}

$gem install bundler
$bundle update
$bundle install

{% endhighlight %}

<br>

### 3-3. Jekyll 블로그 실행

{% highlight shell %}

$bundle exec jekyll serve

...

Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.

{% endhighlight %}

 http://127.0.0.1:4000/로 접속했을 때, 아래와 같은 화면이 나온다면 성공이다.

![Success executing Jekyll Blog]({{ site.baseurl }}/assets/img/initpage.png)