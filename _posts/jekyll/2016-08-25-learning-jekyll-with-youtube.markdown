---
layout: post
title:  "Youtube로 Jekyll을 배워보자 - 2 -"
date:   2016-08-25 08:42:00 +0900
categories: Jekyll
tags : jekyll
---
[이전 글 보기][post_1]  
[다음 글 보기][post_3]

이번 화 관련 영상들

[Jekyll:highlighting navigation][lecture_12]

[Jekyll:include parameters][lecture_13]

[Jekyll:looping over posts][lecture_14]

제어문과 파라미터 전달에 대해서 확인할 수 있는 강의다.

{% highlight liquid %}

  {{ "{% if 조건" }} %}

  ...

  코드

  ...

  {{ "{% endif" }} %}

{% endhighlight %}

위의 코드가 Jekyll의 if 문이다. 별 거 없다.

for문도 마찬가지로 별 거 없다.

{% highlight liquid %}

{{ "{% for post in posts" }} %}
  {{ "{% if post.url" }} %}
    <li><a href=" {{ "{{ site.baseurl" }} }} {{ "{{ post.url" }} }}">{{ "{{ post.title"}} }}</a></li>
  {{ "{% endif" }} %}
{{ "{% endfor" }} %}

{% endhighlight %}

위 코드는 posts 를 순회하면서 모든 post를 출력하는 [category 페이지]({{ site.baseurl }}/category/)에서 사용된 루프의 일부이다.


[post_1]:{{ site.baseurl }}{% post_url 2016-08-24-learning-jekyll-with-youtube %}
[post_3]:{{ site.baseurl }}{% post_url 2016-08-27-learning-jekyll-with-youtube %}
[lecture_12]:https://www.youtube.com/watch?v=T7ApyjWO3nQ&index=12&list=PLWjCJDeWfDdfVEcLGAfdJn_HXyM4Y7_k-
[lecture_13]:https://www.youtube.com/watch?v=TJcn_PJ2100&list=PLWjCJDeWfDdfVEcLGAfdJn_HXyM4Y7_k-
[lecture_14]:https://www.youtube.com/watch?v=9ePPr5rOszc&index=14&list=PLWjCJDeWfDdfVEcLGAfdJn_HXyM4Y7_k-
