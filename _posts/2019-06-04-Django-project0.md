---
layout: post
title: "[Django 프로젝트] 메모 앱 만들기 - 프로젝트 명세"
subtitle: "Django 메모장 프로젝트 시작하기"
categories : Django
tags: [Django, Project]
author: Nayeong Kim
comments: True
---
<div id='preview' class='display-none'>
개인적인 Django 프로젝트를 고민하다가 '인스타그램'과 '메모장'을 만들기로 결정했다. 메모장을 구현하기에 앞서 기능 명세를 작성했다.
</div>

## 메모장 프로젝트 명세

그동안 공부했던 Django를 복습하는 프로젝트로 간단한 메모장을 만들어보고자 한다.

<br/>

### 1. 프로젝트 기능

- 필수
   - [ ] &nbsp;&nbsp;로그인, 로그아웃
   - [ ]  &nbsp;&nbsp;메모 추가/삭제/수정
   - [ ]  &nbsp;&nbsp;좋아요 기능
   - [ ]  &nbsp;&nbsp;조회(생성일자, 작성자, 좋아요, 태그) 기능
   - [ ]  &nbsp;&nbsp;내가 쓴 메모 조회 기능

- 추가
   - [ ]  &nbsp;&nbsp;태그 기능
   - [ ] &nbsp;&nbsp;소셜로그인(Google, Github)

<br/>

### 2. 개발 및 배포

- 개발환경
   - Language : Python(3.6.7),
   - Framework : Django(2.2), Vue.js, django-restframework

- 배포환경
   - Heroku 또는 EC2
