---
layout: post
title:  "제네릭 (무공변성, 공변성, 반공변성)"
summary: ""
author: byunjiwoon
date: '2024-02-19 00:00:00 +0530'
category: flutter
thumbnail: 
keywords: 
permalink: 
usemathjax: true 
---

제네릭이란?
--- 

클래스, 함수에서 매개변수에 사용되는 자료형을 개체 생성 시 정한다


타입 캐스팅 필요가 없어 안정성을 높일 수 있다.
타입의 범위를 지정할 수 있는데 이것을 타입 바운드라고 한다

타입 바운드
---
1. 불변성
2. 공변성
3. 반공변성             
        
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


```kotlin
class Cage<T> {

}

```

Cage<Bird>, Cage<Eagle> 가 서로 상속관계라고 생각할 수 있지만
서로 아무 관계도 아니다!
Cage는 무공변, 불공변하다 라고 표현할 수 있다


```
val bird = Bird()
val eagle = Eagle()
val penguin = Penguin()

val cage = Cage<Bird>()

```
위 개체들을 Cage<Bird> 에 담으려면 
아래 처럼 해주면 된다.

```kotlin
class Cage<out Bird> {

}

```
자기자신과 자식 객체를 허용하려면  out Bird 를 입력한다
이것을 공변성이라고 하고
반대로 자기 자신과 부모 객체만 허용한다는 것은 반공변성이라고 한다


