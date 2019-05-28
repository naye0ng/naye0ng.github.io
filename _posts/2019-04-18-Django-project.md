---
layout: post
title: "[Django 프로젝트] 메모 앱 만들기 1 - 프로젝트 및 앱 생성"
subtitle: "Django 프로젝트 및 앱 생성"
categories : Django
tags: [Django, Project]
author: Nayeong Kim
comments: True
---

개인적인 Django 프로젝트를 고민하다가 '인스타그램 클론 코딩'과 '메모장 앱'을 만들기로 결정했다. 비교적 간단하다고 생각한  '메모장 앱'의 기능들을 나열하고 보니, 생각보다 복잡해질 것 같아 걱정이다.

<br>

### 메모 앱 기능 정리

[ Django ]
- [ ]  &nbsp;&nbsp;개인 메모
- [ ]  &nbsp;&nbsp;단체 메모
- [ ]  &nbsp;&nbsp;좋아요 기능
- [ ]  &nbsp;&nbsp;태그 기능
- [ ]  &nbsp;&nbsp;색상 및 테두리 변경 기능
- [ ]  &nbsp;&nbsp;강조 기능
- [ ]  &nbsp;&nbsp;조회(생성일자, 작성자) 기능
- [ ]  &nbsp;&nbsp;소셜 로그인(Google, GitHub)

[ Javascript ]

- [ ]  &nbsp;&nbsp;사용자 UI 개선
- [ ]  &nbsp;&nbsp;좋아요, 색상 등을 비동기적으로 처리
- [ ]  &nbsp;&nbsp;마우스 이벤트로 메모 위치 이동 및 고정

<br>

## Django 프로젝트 및 앱 생성

AWS Ubuntu 환경에서 작업할 예정이며, 이와 관련된 내용은 [[aws]Django 서버 세팅1]({{ site.baseurl}}/2019/04/15/AWS-EC2-Ubuntu-인스터스-생성-및-Django-서버-세팅.html),  [[aws]Django 서버 세팅2]({{ site.baseurl}}/2019/04/15/AWS-EC2-Ubuntu-인스터스-생성-및-Django-서버-세팅-2.html) 에서 확인할 수 있다.

<br>

### 1) Django 프로젝트 생성
[[aws]Django 서버 세팅2]({{ site.baseurl}}/2019/04/15/AWS-EC2-Ubuntu-인스터스-생성-및-Django-서버-세팅-2.html) 에서 이미 pyenv, virtualenv 설치 및 Django 프로젝트를 생성했으므로 중요한 부분만 다시 정리한다.

{% highlight shell %}
# 프로젝트 이름의 폴더 생성 및 이동
$mkdir {프로젝트명}
$cd {프로젝트명}

# 현재 폴더를 가상화하여 독립된 공간으로 만든다.
$pyenv local practice-venv

# 가상환경 안에 django 설치
# 여기서 중요한 점은 pyenv virtualenv로 독립된 가상환경을 만들었으므로 해당 폴더 안에서만 django가 설치된다.
$pip install django

# pip 설치 패키지 목록에 django 설치 확인
$pip list
Package    Version
---------- -------
Django     2.2
pip        19.0.3
pytz       2019.1
setuptools 39.0.1
sqlparse   0.3.0

# 프로젝트 생성
# 현재 위치(.)에 여러 파일(프로젝트)이 자동으로 생성된 것을 확인할 수 있다.
$django-admin startproject {프로젝트명}  .
{% endhighlight %}
 <br>
#### settings.py 기본 설정
프로젝트를 생성하고 나면 프로젝트 폴더 아래에 Django의 setting.py가 생성된다. 
{% highlight python %}
# Public DNS가 'https://{}.compute.amazonaws.com'라면 https://는 제거
ALLOWED_HOSTS = ['{}.compute.amazonaws.com']

# 현재 시간 설정
TIME_ZONE = 'Asia/Seoul'

# 언어 설정
LANGUAGE_CODE = 'ko-kr'
{% endhighlight %}

<br>

### 2) Django 앱 생성
{% highlight shell %}
$python manage.py startapp {앱이름}
{% endhighlight %}
성공적으로 앱이 생성되었다면 앱이름의 폴더가 생성됨을 확인할 수 있다.
 
 <br>

#### settings.py 앱 설정 추가
Django 패키지를 설치하거나 앱을 생성하고 나면 설정 파일에 명시해줘야 한다.
{% highlight python %}
INSTALLED_APPS = [
   ...,
   '{앱이름}',
]
{% endhighlight %}

여기까지는 nano에디터로 코드를 수정하는데 문제가 없었지만 앞으로 복잡한 기능을 구현하기에 nano에디터는 적합하지 않다. vscode 혹은 pycharm에디터에서 제공하는 ftp기능을 사용하자.

<br>

<br>









