---
layout: post
title:  "Spring으로 JSON을 쐈는데 글자가 깨지는 경우"
date:   2016-10-24 00:20:00 +0900
categories: spring
tags: spring
---
### 이유가 너무 많다

서버 - 프론트 통신에서 글자가 깨지는 이유는 한 마디로 "인코딩이 달라서"로 요약할 수 있지만 문제는 인코딩 문제가 생기는 지점이 너무 많다는 것이다.  
어쩌겠는가? CJK 월드에 사는 이상 인코딩 문제는 항상 안고 가야 하는 것을...  

### jQuery Ajax는 기본이 UTF-8이다

[XMLHttpRequest을 직접 사용하더라도 form의 accept-charset 속성을 조작하지 않으면 UTF-8로 보내도록 되어있긴 한데][w3c-form] 이 규칙은 Document의 Charset이 지정되어 있을 경우에는 Document를 따르도록 되어 있기 때문에 (그리고 구형 IE는 저 속성을 잘 읽지 못하기 때문에) 기본적으로 <b>HTML 문서의 Charset 설정을 반드시 확인</b>해야 한다.

### HTML 파일의 인코딩은 어떤가?

Document의 Charset과 별도로 <b>프론트엔드 페이지 파일이</b> 어떤 문자셋으로 되어있는지도 확인해야 한다. 서버랑 다른 인코딩을 쓰고 있다면 ajax나 post로 값을 넘길 때 문자가 박살나는 것을 볼 수 있다.  

### DB의 기본 인코딩은 어떤가?

만약 DB가 EUC-KR 같은 걸로 되어 있고 서버가 UTF-8을 쓰는 식으로 서로 인코딩이 다르다면 서버에서 DB 값을 뽑아올 때도 이상한 값이 찍히는 것을 확인할 수 있다.  
문제는 DB가 서버와 같은 인코딩으로 되어 있더라도 가끔 문제가 생기는 경우가 있다는 점이다. 이 때는 <b>서버에서 DB에 접속할때 커넥션의 인코딩을 강제로 지정해야</b> 문제가 생기지 않는다.  

DB커넥션 옵션은 서버 언어와 DB접속에 사용하는 클래스 등에 의해 다양하기 때문에 반드시 관련 문서를 읽어보면서 파악해야 한다.  
예컨대 spring boot application의 경우 spring.datasource.url 속성에 get 파라미터로 characterEncoding=UTF-8 를 넘길 수 있다.  

DB인코딩 문제는 서버가 옛날에 만들어진 경우에 자주 나타난다. 서버 파일을 열었는데 자체 개조된 제로보드 레거시 코드 같은게 주르륵 나온다면? 축하합니다. 당첨 되겠습니다.

### JSON Builder부분에 문제가 있을 때 <-- 이번에 삽질한 부분

정말 미치고 팔짝 뛰는 문제가 아닐 수 없다. 서버에서 JSON을 println으로 찍어도 제대로 나오고 프론트도 인코딩을 맞춰놨는데 ajax만 쏘면 한글이 개박살난다.  

spring 에서 RequestMapping을 처리하는 함수의 인자로 HttpServletResponse response 파라미터를 받게 될 텐데, JSONObject 를 사용할때 반드시 아래 코드를 함께 써야 한다.  

<b>response.setCharacterEncoding("UTF-8");</b>

이걸 몰라서 얼마나 삽질을 했는지...

[w3c-form]:https://www.w3.org/TR/html5/forms.html#application/x-www-form-urlencoded-encoding-algorithm
