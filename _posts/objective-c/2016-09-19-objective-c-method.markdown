---
layout: post
title:  "Objective-C 메소드는 왜 이런 식으로 생겼나?"
date:   2016-09-19 22:28:00 +0900
categories: Objective-C
tags: objective-c
published: false
---
[Objective-C 함수 문법 설명][how-to-obj-c-method]  

C나 Java를 통해 프로그래밍에 입문하는 경우가 많고 요즘에는 Python도 슬슬 주가를 올리고 있지만 어쨌거나 이 언어들은 함수 선언과 호출이 상당히 닮은 편이다.  

위 링크의 설명을 빌려오자면
{% highlight c %}
  void DriveCar(Car car, Person person);
{% endhighlight %}

이런 C나 Java 코드는 꽤 익숙한 것이다.  

그런데 같은 내용을 Objective-C로 표현하면  

{% highlight Objective-C %}
- (void)driveCar:(Car *)car withPerson:(Person *)person;
{% endhighlight %}

이런 식으로 표현되는 것이다.

Objective-C는 C의 슈퍼셋이라며...?  

사실 위의 Objective-C 함수는 아래와 같이 써도 동일하게 동작한다.

{% highlight Objective-C %}
- (void)driveCar:(Car *)car :(Person *)person;
{% endhighlight %}

이제 C랑 비슷하긴 한데 그래도 좀 이상하지 않은가?  

어차피 함수 구현부에서 접근할 수 있는 파라미터는 car와 person 뿐이고 : 앞의 withPerson은  라벨에 불과한데 말이다. 특히 driveCar 같은 경우에 C나 Java의 함수명과 일맥상통하기 때문에 뒤에 오는 withPerson과 달리 생략할 수 없는 특징이 있는데, 그럼에도 불구하고 (계속)

[how-to-obj-c-method]:http://roadfiresoftware.com/2014/06/how-to-read-and-write-method-declarations-in-objective-c/
