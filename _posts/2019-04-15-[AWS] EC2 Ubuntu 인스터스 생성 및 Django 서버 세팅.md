---
layout: post
title: "[AWS] EC2 Ubuntu 인스터스 생성 및 Django 서버 설정 1"
subtitle: "EC2 인스턴스 생성 및 설정"
tags: [AWS, Django]
author: Nayeong Kim
---
<div id='preview' class='display-none'>
EC2 Ubuntu 인스턴스를 생성하고, root계정을 활성화하여 접속하기
</div>

## 1. EC2 Ubuntu 생성 및 접속
### 1). 인스턴스 선택
EC2 Dashboard > Instance > Lalunch Instance 클릭한 후, Ubuntu를 검색하면 아래와 같은 화면이 나타난다.

![Lalunch_Instance1]({{ site.baseurl }}/assets/img/instance01.png)

<br>

select 버튼을 누르고 아래와 같이 free tier 인스턴스를 선택하고 next버튼을 누른다.

![Lalunch_Instance2]({{ site.baseurl }}/assets/img/instance02.png)
<br>

### 2). 보안그룹 설정
기본적으로 인스턴스 생성시 ssh 접속을 위한 22번 포트는 설정되어 있다.
이 외에 사용자가 Django 웹에 접근할 수 있도록 하기 위해 http 접속을 위한 80포트와 Django의 8000포트를 추가로 열어줘야한다.

![Lalunch_Instance3]({{ site.baseurl }}/assets/img/instance03.png)
&#8251; *runserver를 통해 8000포트가 아닌 80포트로 연결하는 것도 가능하다.*

<br>

### 3). Key pair 생성
키페어는 ssh를 통해 EC2 인스턴스에 접속 할 때 사용되며, 이때 생성되는 private key는 한 번만 다운로드 가능하다.(이미 사용하고 있는 key를 그대로 사용하는 것도 가능)

![Lalunch_Instance4]({{ site.baseurl }}/assets/img/instance04.png)

<br>

### 4). ssh로 EC2 접속
터미널 창에 ssh -i 명령어를 사용하여 EC2에 접속한다.
{% highlight shell %}
$sudo ssh -i {키페어 저장 경로}/{키패어 파일} ubuntu@{Public DNS}
# 아래와 같이 출력되면 접속 성공
Welcome to Ubuntu 18.04.2 LTS (GNU/Linux 4.15.0-1032-aws x86_64)
...
41 updates are security updates.

ubuntu@{ip 정보}:~$
{% endhighlight %}
Public DNS는 instance 메뉴에서 확인 가능하다.

![Lalunch_Instance5]({{ site.baseurl }}/assets/img/instance05.png)

<br> 

## 2. [선택] root 계정 활성화
기본적으로 EC2의 root계정은 비활성화 되어 있다. 이전에 root계정을 활성화하지 않고 개발을 진행하다가 프로세스 문제가 생겼던 적이 있어서, root 계정을 활성화 하기로 했다.

### 1). root 사용자 생성
{% highlight shell %}
# root 사용자 생성, 원하는 비밀번호를 입력한다.
ubuntu@{ip 정보}:~$ sudo passwd
# root 사용자로 접속하면, 사용자가 ubuntu에서 root로 바뀐다.
ubuntu@{ip 정보}:~$ su
root@{ip 정보}:~$
{% endhighlight %}

<br>

### 2). sshd_config 설정 변경
{% highlight shell %}
# 나노 에디터로 ssh설정을 변경한다.
$ sudo nano /etc/ssh/sshd_config
{% endhighlight %}

**[변경 전]**
{% highlight shell %}
#LoginGraceTime 2m
#PermitRootLogin prohibit-password
#StrictModes yes
#MaxAuthTries 6
#MaxSessions 10
{% endhighlight %}

**[변경 후]**
<br>
**PermitRootLogin prohibit-password** 부분을 찾아서 주석을 해제하고 옵션을 변경한다.
{% highlight shell %}
#LoginGraceTime 2m
PermitRootLogin yes
#StrictModes yes
#MaxAuthTries 6
#MaxSessions 10
{% endhighlight %}

<br> 

### 3). Ubuntu 개인키(authorized_keys) 복사
Ubuntu 기본 사용자 개인키를 루트 계정으로 복사한다.
{% highlight shell %}
$sudo cp /home/ubuntu/.ssh/authorized_keys /root/.ssh
{% endhighlight %}

<br>

### 4). SSH 재시작
{% highlight shell %}
# 재시작
$sudo service ssh restart
# 접속 종료
$exit
{% endhighlight %}

<br>

### 5). Root 계정으로 접속
{% highlight shell %}
$sudo ssh -i {키페어 저장 경로}/{키패어 파일} root@{Public DNS}
# 아래와 같이 root계정으로 로그인이 가능하다.
root@{ip 정보}:~$
{% endhighlight %}

<br>
