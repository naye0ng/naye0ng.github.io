---
layout: post
title: "빅스비 캡슐 개발 시작하기"
subtitle: "출구찾기 빅스비 캡슐 만들기"
tags: Bixbys
author: Nayeong Kim
comments : True
---

# Bixby 시작하기

2019 삼성 빅스비 경진대회 제출용으로 출구찾기 앱을 기획하였다. 본격적인 개발에 앞서 빅스비 캡슐의 구조를 파악하고 정리한 내용이다.



## 1. Bixby 구조

resources/ : 언어 설정, 레이아웃, 트레이닝, 엔드포인트 정보가 들어간다.

models/concept/ : 변수 타입 및 연산자 정의한다.

models/actions/ : 빅스비 캡슐의 전체적인 역할(함수)을 정의한다.

code/ : 실제 작동하게 될 연산을 javascript로 구현한다.



