---
layout: post
title:  "Youtube로 Jekyll을 배워보자 - 4 -"
date:   2016-08-30 08:30:00 +0900
categories: jekyll
---
[이전 글 보기][post_3]  
[다음 글 보기][post_5]  

이번 화 관련 영상들

[Jekyll: using posts for ordered content][lecture_20]

[Jekyll: data files][lecture_21]

20화는 기존에 잘 알려진 튜토리얼대로 YAML 선언부의 categories 변수를 이용한 루프를 소개하고 있는데, 21화에서는 흥미롭게도 \_data 폴더를 통해서 category를 루프하는 효과를 낼 수 있다고 한다.

자세한 내용은 [공식 문서](https://jekyllrb.com/docs/datafiles/)를 읽어보면 확인할 수 있다.

예를 들어 나는 \_data\game 디렉토리  밑에 info.json 이라는 파일을 만들었다. \_data 디렉토리의 하위 디렉토리는 그대로 네임스페이스가 된다. 이 경우 데이터에 접근하기 위해서는 site.data.game.info 라고 입력하면 된다.

과거에는 데이터 파일 형식으로 .yml을 선호했다고 하는데 최신 버전 Jekyll에서는 문제없다고 하니 json, csv, yml 중에서 편한 대로 골라쓰면 되겠다.


### info.json

{% highlight json %}

[
  {
    "title":"Rust",
    "developer": "Facepunch Studios",
    "publisher": "Facepunch Studios",
    "release_date": "12 Dec, 2013"
  },
  {
    "title":"Overwatch",
    "developer": "Blizzard Entertainment",
    "publisher": "Blizzard Entertainment",
    "release_date": "24, May, 2016"
  }
]


{% endhighlight %}

다음과 같이 데이터를 순회하면

### topic.html

{% highlight liquid %}

{{ "{% for game_info in site.data.game.info" }} %}
  <ul><h4 class="post-sub-title">{{ "{{game_info.title" }} }}</h4>
    <li>Title : {{ "{{ game_info.title" }} }}</li>
    <li>Developer : {{ "{{ game_info.developer" }} }}</li>
    <li>Publisher : {{ "{{ game_info.publisher" }} }}</li>
    <li>Release Date : {{ "{{ game_info.release_date" }} }}</li>
  </ul>
{{ "{% endfor" }} %}

{% endhighlight %}

아래의 결과처럼 json으로부터 추출된 내용이 html로 출력된다.

{% highlight html %}

{% for game_info in site.data.game.info %}
  <ul><h4 class="post-sub-title">{{ game_info.title }}</h4>
    <li>Title : {{ game_info.title }}</li>
    <li>Developer : {{ game_info.developer }}</li>
    <li>Publisher : {{ game_info.publisher }}</li>
    <li>Release Date : {{ game_info.release_date }}</li>
  </ul>
{% endfor %}

{% endhighlight %}

[post_3]:{{ site.baseurl }}{% post_url 2016-08-27-learning-jekyll-with-youtube %}
[post_5]:{{ site.baseurl }}{% post_url 2016-09-06-learning-jekyll-with-youtube %}
[lecture_20]:https://www.youtube.com/watch?v=yLptLUVoz3k&list=PLWjCJDeWfDdfVEcLGAfdJn_HXyM4Y7_k-
[lecture_21]:https://www.youtube.com/watch?v=1rXBzPiSa5c&list=PLWjCJDeWfDdfVEcLGAfdJn_HXyM4Y7_k-
