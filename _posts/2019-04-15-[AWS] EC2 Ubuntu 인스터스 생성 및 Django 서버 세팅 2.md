---
layout: post
title: "[Instagram clone] EC2 Ubuntu 인스터스 생성 및 Django 서버 설정 2"
subtitle: "Ubuntu에 pyenv, virtualenv 설치 및 서버 실행"
tags: [AWS, Django]
author: Nayeong Kim
---
<div id='preview' class='display-none'>
Ubuntu기반의 서버에 Django 가상환경(pyenv, virtualenv) 설정 및 서버 실행하기
</div>


## 1. Ubuntu에서 pyenv, virtualenv 설치
Python은 2.x와 3.x버전 사이에 지원하는 기능의 차이가 많아 버전관리 문제가 있다. 그래서 대부분의 python 사용자들은 pyenv와 virtualenv를 사용하여 가상환경을 생성하고 python 버전을 관리한다.

패키지 설치하기 전에 아래와 같이 업데이트를 해주도록 하자.
{% highlight shell %}
sudo apt-get update
{% endhighlight %}

<br>

### 1). build 패키지 설치
Ubuntu에서 Build 할 때 공통적으로 발생하는 문제를 방지하기 위해 필요한 패키지들을 설치해 준다.
{% highlight shell %}
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev
{% endhighlight %}

<br>

### 2). pyenv, virtualenv 설치 
**pyenv** 란 다양한 버전의 python을 설치할 수 있도록 하는 라이브러리이며, pyenv를 이용하면 원하는 버전의 python을 로컬에 설치할 수 있다.

**virtualenv** 란 서로 다른 종류의 python버전을 관리하는 관리자이며, 여러 개의 python버전을 로컬에서 사용할 수 있도록 한다.

죽, pyenv로 원하는 python버전을 설치하고, virtualenv로 구성한 가상환경에서 사용자가 원하는 python 버전을 사용할 수 있다.
{% highlight shell %}
# pyenv install
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bashrc

# shell reload
exec "$SHELL"

# pyenv-virtualenv install
git clone https://github.com/pyenv/pyenv-virtualenv.git $(pyenv root)/plugins/pyenv-virtualenv
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc
exec "$SHELL"
{% endhighlight %}

<br>

## 2. python 가상환경 설정
### 1). pyenv로 python 3.6.7 설치
{% highlight shell %}
$ pyenv install 3.6.7

# 전역환경에서의 python버전 설정
$ pyenv global 3.6.7
$ python --version
Python 3.6.7
{% endhighlight %}

<br>

### 2). virtualenv로 가상환경 설정
{% highlight shell %}
# 앞서 pyenv로 설치한 3.6.7버전을 사용하는 가상환경을 생성한다.
$pyenv virtualenv 3.6.7 {가상환경이름}

# 가상환경 목록 확인, 앞서 생성한 가상환경이 보이면 성공
$pyenv virtualenvs
{가상환경이름}

# 가상환경을 실행할 폴더를 만들어주자
$mkdir {폴더명}
$cd {폴더명}

# 가상환경 만들기
{가상환경 실행 폴더}$pyenv local {가상환경이름}
(가상환경이름)$
{% endhighlight %}
pyenv local 명령을 수행한 후, 이 폴더에 접속하면 자동으로 가상환경으로 접속된다.

<br>

## 3. Django 프로젝트 생성 
### 1). 가상환경안에 django 설치
pyenv와 virtualenv로 독립된 가상환경을 만들었으므로 해당 폴더 안에서만 django가 설치된다.
{% highlight shell %}
$pip install django
{% endhighlight %}

<br>

### 2). Django 프로젝트 생성
현재 디렉토리(가상환경)에 프로젝트를 생성한다.
<br>
맨뒤에 '.'을 붙여야 하위 폴더가 생성되지 않고, 현재 위치에 바로 프로젝트가 생성(managy.py가 현재 위치에 설치 됨)된다.
{% highlight shell %}
$django-admin startproject {프로젝트명} .
{% endhighlight %}
현재 폴더에 managy.py와 생성한 프로젝트 폴더가 생성된 것을 확인 할 수 있다. 전체적인 구조는 아래와 같다.
{% highlight shell %}
.
├── manage.py
└── {프로젝트명}
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
{% endhighlight %}

<br>

## 4. Django 서버 실행
### 1). ALLOWED_HOSTS 설정
settings.py에 ALLOWED_HOSTS의 값을 EC2의 Public DNS로 설정해야만 외부 사용자가 해당 DNS를 통해 접속할 수 있다.
<br>
나노 에디터를 사용하여 settings.py를 수정하자.
{% highlight shell %}
$nano {프로젝트명}/settings.py
{% endhighlight %}
주의 할 점은 EC2의 Public DNS의 값이 'https://ec2-{}.compute.amazonaws.com'라면 아래와 같이 https://는 제거하고 넣어준다.
{% highlight python %}
# settings.py
ALLOWED_HOSTS = ['c2-{}.compute.amazonaws.com']
{% endhighlight %}

<br>

### 2). Django 서버 실행
{% highlight shell %}
$python manage.py runserver 0.0.0.0:8000

Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).
April 15, 2019 - 10:33:03
Django version 2.2, using settings 'nayeong.settings'
Starting development server at http://0.0.0.0:8000/
Quit the server with CONTROL-C.
{% endhighlight %}

이제 어디에서든 ALLOWED_HOSTS에 설정해준 주소와 8000번 포트를 이용해 Django 서비스에 접속 할 수 있다.
<br>
https://ec2-{본인의 EC2 DNS 참고}.compute.amazonaws.com:8000로 접속했을 때 아래와 같은 화면이 나온다면 성공이다.
![First Django Start]({{ site.baseurl }}/assets/img/firstDjango.png)

만약 runserver 명령어 실행시 아래와 같은 에러가 뜬다면 migrate 하고 다시 서버를 실행시키자.
![runserverErr]({{site.baseurl}}/assets/img/runserver.png)

{% highlight shell %}
$python manage.py migrate
{% endhighlight %}

<br>
<hr>
<br>

#### [추가] 80번 포트로 Django 실행하기
Django는 기본적으로 8000번 포트로 실행되는데, 80 포트로 접속을 허용하고 싶다면 아래와 같은 명령어를 사용하면 된다.
{% highlight shell %}
$python manage.py runserver 0.0.0.0:80

Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).
April 15, 2019 - 10:33:03
Django version 2.2, using settings 'nayeong.settings'
Starting development server at http://0.0.0.0:8000/
Quit the server with CONTROL-C.
{% endhighlight %}

<br>