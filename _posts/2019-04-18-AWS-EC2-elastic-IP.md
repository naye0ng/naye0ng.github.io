---
layout: post
title: "AWS EC2 인스턴스 고정IP 할당"
subtitle: "EC2 인스턴스 IP 고정하기"
categories : AWS
tags: AWS
author: Nayeong Kim
comments : True
---
<div id='preview' class='display-none'>
EC2에 기본적으로 할당된 IP, DNS는 고정된 값이 아니므로 이를 고정하여 Oauth api, ssh 접속을 더 쉽게 만들어보자.
</div>

# AWS Elastic IP 생성 및 연동
EC2에 기본적으로 할당된 IP, DNS는 고정된 값이 아니다. 인스턴스를 정지하거나 삭제한 뒤 새로 만들면(이전의 인스턴스 이미지로) 접속 가능한 IP, DNS는 변경된다.

<br>

### 1) AWS Elastic IP 생성
EC2 Dashboard > Elastic IP > Allocate new address > Allocate를 클릭하면 아래와 같이 IP가 생성된다. 
<br>
(맘에 드는 혹은 외우기 쉬운 IP가 나올 때까지 삭제하고 다시 생성해도 된다.)

![AWS Elastic IP1]({{ site.baseurl }}/assets/img/elasticIP01.png)

<br>

### 2) AWS Elastic IP, EC2 연동
1)에서 생성한 고정 IP를 클릭하고 Associate address를 클릭한다. 아래와 같은 화면에서 연결하고 싶은 인스턴스를 선택하여 연결해준다.

![Lalunch_Instance2]({{ site.baseurl }}/assets/img/elasticIP02.png)

이제 조금만 기다리면 인스턴스 IP가 변경되는 것을 확인할 수 있다.

<br>

*Free Tier계정은 Elastic IP를 무료로 1개까지 사용이 가능하다. 그런데 주의할 점은 **Elastic IP 생성 후 인스턴스와 연결해주지 않으면 한달에 4000원 가량의 과금이 발생**할 수 있다.*

<br>

