---
layout: post
title:  "button 태그는 a 태그 안에 있어도 되는가?"
date:   2016-09-08 01:11:00 +0900
categories: html
tags: html
---
[스택 오버플로우 질문 보러가기][can-i-nest]

### 상황

IE11 에서 테스트하는 상황이었다. form 태그 안에 a 태그가 있고, 이 a 태그는 button을 감싸고 있다. button을 사용한 이유는 vertical-align이 편하기 때문이다.  
vertical-align도 포스팅 하나짜리 주제는 되는데, 아무튼 한 줄짜리 내용물을 세로 중앙 정렬 하는데는 경험상 button이 상당히 편하다. "세로중앙 정렬할 한 줄짜리가 여럿"이면 table도 나쁘지 않다.(물론 아닌 경우도 아주 많다. 그때는 line-height를 쓴다)  

form 안에 button 태그를 위치시킬 때 일반적인 주의점은 type="button" attribute를 안 줄 경우에 자동으로 type="submit"으로 해석하는 경우가 있다는 것이다. 예컨대 회원가입 form 이라면 "주소찾기" 버튼을 눌렀는데 양식을 서버로 쏴버리는 곤란한 장면이 연출될 수 있다.

아무튼 a 태그가 button을 감싸고 있고 button에는 별다른 이벤트 리스너가 걸려있지 않으므로 a 태그에 의해 링크 주소가 새 탭을 띄우는 것이 구현 목표였다. 테스트 해 보니 Chrome이나 Edge에서는 문제없이 돌아가던 것이 IE11에서는 갑자기 먹통이었다. 처음엔 IE가 그렇지 뭐... 하다가 이 구조가 희한하다는 생각을 하게 되었다.  

어쨌거나 button은 "뭔가 일어날 것"을 기대하는 UI다. div나 span이 아니라 button을 썼다는 것은 자연스럽게 click 이벤트와 연결되지 않는가? 그렇다면 a 태그와 button 태그는 역할이 겹치는 경우가 나오게 되는데 위에서 예로 든 회원가입 양식이 대표적인 예다.

a 태그가 새 탭에서 링크 페이지를 띄우도록 구현한 것이 특수한 케이스고 만약 두 엘리먼트가 똑같이 location 점프에 관한 것이라면 a가 먼저냐 button이 먼저냐에 의해 나머지 한 쪽 링크는 아예 무시하는 결과가 된다.

이런 모호성과 중복은 프로그램에서 반드시 제거해야 하는 종류의 것이다.

### 결론

a 태그의 children은 상호작용이 없는 요소만 가능하다.

[can-i-nest]:http://stackoverflow.com/questions/6393827/can-i-nest-a-button-element-inside-an-a-using-html5
