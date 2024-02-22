---
layout: post
title:  "무공변"
summary: ""
author: byunjiwoon
date: '2024-02-19 00:00:00 +0530'
category: flutter
thumbnail: 
keywords: 
permalink: 
usemathjax: true 
---



상위 클래스 Bird
하위 클래스 Eagle , Penguin

있다고 가정하자

상위 타입이 들어가는 자리에는 하위타입이 대신 위치할 수 있다.


```kotlin

fun enterCage(bird : Bird) {

}

val eagle = Eagle()
enterCage(eagle) // eagle은 bird의 하위 타입이므로 가능.


```

하지만

Cage 라는 새장 클래스가 있다고 가정하면

Cage<Bird>, Cage<Eagle> 로 정의된 객체들은 서로 아무 관계도 아니다!
Cage는 무공변, 불공변하다 라고 표현할 수 있다





