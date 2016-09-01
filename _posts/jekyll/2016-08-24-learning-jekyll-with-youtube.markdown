---
layout: post
title:  "Youtube로 Jekyll을 배워보자 - 1 -"
date:   2016-08-24 05:11:00 +0900
categories: jekyll
---
[이전 글 보기][post_0]  
[다음 글 보기][post_2]

이번 화 관련 영상들

[jekyll:layouts][lecture_07]

[jekyll:creating navigation][lecture_08]

[jekyll:includes][lecture_10]

[jekyll Tip:file structure][jekyll-tip-file-structure]


jekyll에는 몇 가지 기본 디렉토리가 있다. _include, _layouts, _posts, _site, _sass 등인데 이 중에서 반복적으로 등장하는 페이지 템플릿을 _layouts 폴더에 넣어 놓으면 Jekyll이 자동으로 인식하게 된다.

아래의 예를 살펴보자.
아래 파일은 _layouts/default.html 파일의 내용이다. 자세히 보면 중간중간에 liquid template 태그인 include 를 발견할 수 있다.
이 include 뒤에 오는 파일명은 전부 _includes 폴더 내에 존재하는 파일의 이름으로, include 자리에 해당 파일의 내용이 복사 붙여넣기가 된다.
C나 PHP를 해봤다면 include라는 키워드가 친숙하게 들릴 것이다.
그리고 "content" 라고만 적혀있는 liquid 태그가 있는데 바로 이 부분이 "반복되지 않는 Unique한 부분"이 들어가는 자리다. 블로그 포스팅으로 치면 블로그 내용이 들어가는 부분이 되는 것이다.

{% highlight html %}

<!DOCTYPE html>
<html>

  {{ "{% include head.html" }} %}

  <body>

    {{ "{% include header.html" }} %}

    <div class="page-content">
      <div class="wrapper">
        {{ "{{ content" }} }}
      </div>
    </div>

    {{ "{% include footer.html" }} %}

  </body>

</html>

{% endhighlight %}

_layouts 폴더를 확인해보면 _layouts 폴더에는 default.html 파일 외에도 page.html 파일과 post.html 파일이 더 들어있다. 그리고 page.html 파일이나 post.html 파일도 default.html과 비슷한 구조로 되어 있는데, "컨텐츠가 들어갈 자리에 content 태그만 달려있는" 모습이다.

그렇다면 default.html 의 content 자리에는 상황에 따라 page.html이나 post.html 파일이 달라붙는 다는 것을 알 수 있을 것이다.

그리고 page.html이나 post.html 파일의 content 자리에 진짜 markdown 파일의 내용이 들어가는 것이다.

여기까지 확인하고 느낀 점은 _includes 폴더는 component보다는 조금 큰 개념이고 _layouts 폴더보다는 작은 부품이라는 것이다. 즉 _layouts 폴더의 페이지 템플릿들은 _includes 폴더에 있는 header나 sidebar 등을 조립해서 만들어지고, _layouts 폴더에 있는 페이지 템플릿들이 정적 페이지로 변환되면서 최종적으로 _site 폴더에 산출물을 만든다고 이해하고 있다.

[post_0]:{{ site.baseurl }}{% post_url 2016-08-21-learning-jekyll-with-youtube %}
[post_2]:{{ site.baseurl }}{% post_url 2016-08-25-learning-jekyll-with-youtube %}
[lecture_07]:https://www.youtube.com/watch?v=ra8r2VymK3c&list=PLWjCJDeWfDdfVEcLGAfdJn_HXyM4Y7_k-
[lecture_08]:https://www.youtube.com/watch?v=fX3jpJlaDHI&list=PLWjCJDeWfDdfVEcLGAfdJn_HXyM4Y7_k-
[lecture_10]:https://www.youtube.com/watch?v=lelmLpXbUEo&list=PLWjCJDeWfDdfVEcLGAfdJn_HXyM4Y7_k-
[jekyll-tip-file-structure]:http://jekyll.tips/jekyll-casts/jekyll-file-structure/
