---
layout: post
title:  "FOUT 문제와 해결"
date:   2016-08-26 08:42:00 +0900
categories: CSS
---
[Paul Irish 아조씨 블로그 보러가기][Paul-Irish-FOUT]

[@font-face 관련 정리 잘 된 블로그][font-face]

FOUT이란 Flash of Unstyled Text의 약자로, 커스텀 @font-face를 사용했을 때 페이지를 불러오면 레이아웃이 일순간 뒤틀리는(깜빡거리는) 것처럼 보이는 현상이다.

왜 이런 일이 발생하는가?

홈페이지를 만들 때 Front 개발자들은 스타일시트를 페이지 상단에, 자바스크립트를 페이지 하단에 위치시킨다. 여기에는 역사적이고 경험적인 지혜가 깃들어 있다. 만약 스타일시트가 페이지보다 늦게 로드되면 FOUC, 즉 Flash of Unstyled Contents 문제가 발생하여 img가 원본 사이즈로 표시되다가 크기가 변한다던가 float이 적용되어야 할 block element가 페이지 로딩 초기에 레이아웃을 뭉개다가 호다닥 자기 자리로 돌아가는 등의 난리법석을 보게 된다. 따라서 스타일시트를 <body>보다 먼저 선언하는 것이 좋은 것이다.

한편 자바스크립트는 DOM을 어떻게 조작할지 모르기 때문에 script 태그가 있으면 브라우저는 렌더링을 블로킹 하고 스크립트를 기다리는데 <head>나 심지어 <body> 중간에 script가 존재한다면 렌더링이 방해받기 때문에 당연히 좋지 않다. 따라서 대부분 script는 <body>태그 닫기 직전 등 "없어도 렌더링하는데 상관없는" 곳에 위치하는 것이다.

커스텀 @font-face를 사용했을때 브라우저 입장에서는 난생 처음보는 어떤 폰트를 페이지에 적용하라는 과제가 주어지는데, 불행히도 해당 폰트에 대한 데이터는 @font-face가 선언된 스타일시트를 만나면서 다운로드되기 시작한다. 이 경우 firefox는 "기본 폰트로 렌더링하면서 폰트 다운로드가 완료되면 다시 텍스트를 렌더링"하고, 그 외 브라우저는 "폰트를 렌더링하지 않다가 폰트 다운로드가 완료되면 렌더링을 시작"하는데 바로 여기서 페이지 깜빡임이 발생하는 것이다. 기본 폰트든 공백이든 새롭게 적용될 폰트의 폭과 넓이가 기존에 텍스트들이 차지하고 있던 공간과 다르기 때문에 그에 맞춰서 나머지 element가 이동해야 하기 때문이다.

이 문제를 해결하기 위해서는 Google WebFont Loader를 적용하는 것이 손맛(?)이 좋다.

자세한 내용은 다음 블로그들을 참고하자.

[구글 웹 폰트 빠르게 불러오는 방법](http://blomari.tistory.com/83)

[구글 웹폰트를 빠르게 로드하는 팁 7가지](https://nolboo.kim/blog/2013/10/22/google-web-font-faster-tip/)


[Paul-Irish-FOUT]:http://www.paulirish.com/2009/fighting-the-font-face-fout/
[font-face]:http://www.clearboth.org/font-face_performance/
