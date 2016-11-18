---
layout: post
title:  "SSL3는 POODLE 공격에 취약하다"
date:   2016-08-31 04:20:00 +0900
categories: security
tags: security
---
정리하려고 보니까 이미 잘 된 사이트가 많아서 링크만 걸면 되겠다  
[Poodle :padding oracle on downgraded legacy encryption][Poodle_blog_01]

2014년에 공개되었다는데 오늘 SSL 테스트를 하던 도중에 우연히 취약점 체크에 걸려서 알게 되었다.

보안 쪽 이슈는 전문가가 아니라 자세히 알지 못하지만 훑어보니 대강의 내용은 이해할 수 있었다.  

암호화된 패킷 통신 내용을 감청할 수 있는 것은 물론이고 쿠키를 탈취당할 경우에는 세션 하이재킹이 일어나기 때문에 특히 심각하다고.
공격 기법들을 보면 정말 기발한 발상이 많다.  

### BEAST

POODLE을 사실상 BEAST 위협의 연장으로 보는 시야가 많길래 BEAST 관련 내용도 링크한다.  
[An Illustrated Guide to the BEAST Attack][beast_illust_explain]  
[BEAST attack on SSL/TLS explained][beast_slideshare]  
[Is BEAST Still a Threat?][beast_qualys]

BEAST 공격에 대해 요약하자면 다음과 같다.  
CBC(cipher-block chaining)를 비롯한 블록 방식 암호화 알고리즘은 데이터를 일정한 크기의 블록 단위로 암호화하는데, 이때 첫 블록에 대해서는 IV(initialization vector)가 사용된다.  
IV는 평문과 결합하여 최초의 암호화된 블록을 만들어낸다. CBC의 마지막 C가 chaining인 이유는 이렇게 만들어진 첫 블록의 암호화 결과가 다음 평문과 XOR연산되어 다시 암호문을 만드는 입력으로 사용되기 때문이다.  

그런데 만약 man-in-the-middle 공격을 통해 패킷을 탈취 / 변조 할 수 있는 상태가 되면 SSL 스트림에 공격자가 임의의 패킷을 injection 할 수 있게 된다.  

그리고 XOR 연산은 역원이 자기 자신이므로 A xor B xor B 는 A만 남게 된다. 공격자가 이 성질을 이용해 "이미 XOR된 데이터"를 평문 상태로 입력하도록 패킷을 변조하면 chaining이 반복되면서 중간값을 유추하기 힘들어지는 CBC의 효과를 무력화시키고 자신이 원하는 값을 패킷에 끼워넣거나 IV를 예측할 수 있도록 만든다. 당연히 이런 상황까지 오면 암호화는 깨진 것이다.

### 예방

POODLE공격과 마찬가지로 BEAST공격도 man-in-the-middle 상황을 만들어야 하는 등의 까다로운 조건이 필요하긴 하지만 공용와이파이 등을 통해서 얼마든지 달성할 수 있는 조건이다.  
더욱이 BEAST는 순수하게 클라이언트의 보안 취약성이기 때문에 서버에서 컨트롤하기가 난감하다는 점도 문제다. 현재로서는 서버사이드에서는 SSL 3.0이나 TLS 1.0 이하의 보안 채널을 지원하지 않도록 설정하는 것이 최선으로 보인다. 이 설정은 POODLE 공격에도 유효한 대응책이 된다.

[Poodle_blog_01]:http://shayete.tistory.com/entry/Poodle-padding-oracle-on-downgraded-legacy-encryption
[beast_illust_explain]:http://commandlinefanatic.com/cgi-bin/showarticle.cgi?article=art027
[beast_slideshare]:http://www.slideshare.net/danrlde/20120418-luedtke-ssltlscbcbeast
[beast_qualys]:https://blog.qualys.com/ssllabs/2013/09/10/is-beast-still-a-threat
