---
layout: post
title:  "Objective-C 메소드는 왜 이런 식으로 생겼나요?"
date:   2016-09-19 22:28:00 +0900
categories: Objective-C
tags: objective-c
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

어차피 함수 구현부에서 접근할 수 있는 파라미터는 car와 person 뿐이고 : 앞의 withPerson은  라벨에 불과한데 말이다. 특히 driveCar 같은 경우에 C나 Java의 함수명과 일맥상통하기 때문에 뒤에 오는 withPerson과 달리 생략할 수 없는 특징이 있는데, 그럼에도 불구하고 withPerson 부분과 구조적으로 똑같이 (something) : (variable) 형태를 취하고 있어서 처음에 되게 어리둥절하게 만들었다.

결국 위 링크의 설명을 듣고 깨달은 것은 driveCar:withPerson: 을 함수명으로 생각해야 이해가 쉽다는 것이다. withPerson이 생략 가능한 이유도 이렇게 생각하면 쉽게 이해된다. 라벨 하나가 삭제되어도 함수명 입장에서는 길이가 조금 줄어드는 것에 불과하기 때문이다.

결국 이런 구조를 갖게 된 근원을 파헤치다보면 스몰토크에 도달하게 되는데, 메시지 전달 방식으로 함수를 호출(함수를 호출한다는 표현도 너무 C나 Java 스러운 것인지도 모른다)하려다 보니 스몰토크의 방식을 채용하게 된 것으로 보인다.

이 방식의 장점이자 단점은 인자가 많을 때인데, 가령 3 by 3 행렬의 모든 원소를 기본 자료형으로 해체해서 파라미터로 넘길 때 C에서는 IDE의 도움이 없을 때 9개의 같은 자료형을 나란히 늘어놔야 하므로 매우 헷갈리는데 Objective-C 에서는 label을 명시적으로 적어줄 수 있으므로 헷갈림이 덜하다.

대신 함수 선언부가 무지막지하게 길어져서 마음에 안 들게 되지만...  

[how-to-obj-c-method]:http://roadfiresoftware.com/2014/06/how-to-read-and-write-method-declarations-in-objective-c/
