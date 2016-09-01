---
layout: post
title:  "SSL3는 POODLE 공격에 취약하다"
date:   2016-08-31 04:20:00 +0900
categories: security
---
정리하려고 보니까 이미 잘 된 사이트가 많아서 링크만 걸면 되겠다 (개꿀 ㅎㅎ)  
[Poodle :padding oracle on downgraded legacy encryption][Poodle_blog_01]

2014년에 공개되었다는데 오늘 SSL 테스트를 하던 도중에 우연히 취약점 체크에 걸려서 알게 되었다.

보안 쪽 이슈는 전문가가 아니라 자세히 알지 못하지만 훑어보니 대강의 내용은 이해할 수 있었다.  

암호화된 패킷 통신 내용을 감청할 수 있는 것은 물론이고 쿠키를 탈취당할 경우에는 세션 하이재킹이 일어나기 때문에 특히 심각하다고.
공격 기법들을 보면 정말 기발한 발상이 많다.  

[Poodle_blog_01]:http://shayete.tistory.com/entry/Poodle-padding-oracle-on-downgraded-legacy-encryption
