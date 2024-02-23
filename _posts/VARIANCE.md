---
layout: post
author: byunjiwoon
title: Netlify CMS created this Article
date: 2020-05-23T09:52:20.613Z
thumbnail: /assets/img/posts/hello.jpg
category: jekyll
summary: Demo Content using Netlify CMS
keywords: using netlify cms with devlopr-jekyll, devlopr jekyll netlify cms, how to use netlify cms
permalink: /blog/using-netlify-cms/
---
![alt text](image-1.png)
## OUT
Out 은 다른 곳에서 데이터를 가져올 때만 호출할 수 있다


```kotlin
class Cage<T> {
    fun getFrom(otherCage : Cage<out T>) {
        birds.addAll(otherCage.birds)    
    }
}

```

아래처럼 자신보다 상위클래스는 가져올 수 없다
```kotlin

val cage = Cage<Bird>()
val cage2 = Cage<eagle>()
val cage3 = Cage<penguin>()
val cage4 = Cage<Animal>()

cage.getFrom(cage2) // 가능
cage.getFrom(cage3) // 가능
cage.getFrom(cage4) // 불가능


```
out 을 붙이면 otherCage는 제공하는 역할만 할 수 있다
otherCage 에 put 은 안되는 걸까?
```kotlin
fun getFrom(otherCage : Cage<out T>) {
    otherCage.put(birds[0]) //불가
    otherCage.put(birds[1]) //불가
}
```
out으로 정의 했으니 otherCage는 타입이 같거나 하위클래스일 것이다.
birds[0], birds[1] 는 bird 펭귄인지, 참새인지 어떤 새인지 모르기 때문에
컴파일이 불가능하다
out을 없애면 실행이 허용되지만 타입안정성이 깨지기 때문에 런타임 에러 발생할 수 있다.

## IN

in은 데이터를 set하는데 사용할 수 있다
moveTo 함수를 예를 들어본다

```kotlin

val birdCage = Cage<Bird>()
val eagleCage = Cage<eagle>()

eagleCage.put(Bird())
eagleCage.moveTo(birdCage) // 독수리를 일반 새장으로 보낸다
//이렇게 되려면 Cage<Eagle>이 Cage<Bird> 보다 상위타입이어야한다
이렇게하면 반공변하게 만들어야한다

fun moveTo(otherCage : Cage<in T>) {
    otherCage.birds.addAll(this.birds)
}

```
in을 붙이게 되면 데이터를 받을 수 있다. put 가능


#### out : 함수파라미터에서 공변, 생산자
#### in : 함수파라미터에서 반공변, 소비자
#### 공변 : 타입 파라미터의 상속관계가 제네릭에서도 유지;
#### 반공변 : 타입 파라미터의 상속관계가 제네릭 클래스에서는 반대로 된다