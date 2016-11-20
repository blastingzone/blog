---
layout: post
title:  "Github 페이지용 Jekyll 에서는 post_url사용시 에러에 주의해야 한다"
date:   2016-11-20 22:30:00 +0900
categories: Jekyll
tags : jekyll
---
얼마 전에 jekyll - github - travis-ci 사이의 컴파일 결과가 성공 / 실패로 갈라지는 문제에 대해서 포스팅 했었다.

결국 위 문제를 해결하기 위해 약 2일 정도가 소모되었는데 빠르게 결론부터 시작하자.

## 결론

`가급적 post_url 태그를 사용하지 말라!`

## 이유

post_url 태그는 jekyll 프로젝트의 post간의 링크를 위해 사용한다.  
jekyll은 빌드 도중 post_url 태그를 발견하면 ruby로 html을 생산하면서 해당 포스트를 탐색해서 링크를 제공하는데, 문제는 post상단에 선언한 yaml 값의 timezone에 따라서 포스팅 날짜가 하루 정도 바뀔 수 있다는 점이다. (정확히는 timezone을 제대로 인식하지 못하면 문제가 발생하는 것으로 보인다) [해당 이슈 보러가기][jekyll-post-url-issue]

내 경우 로컬과 travis-ci 에서는 분명 컴파일이 성공하는데 github에 커밋하면 page build failed가 계속되었다.  
이것은 로컬과 travis-ci의 컴파일 환경(정확히는 timezone)이 다행히(?) 문제가 없는 상황이기 때문이다.  
github에서 그동안 문제가 없었던 것은 추측컨대 github jekyll의 빌드 환경이나 버전 등이 위 이슈를 피해가는 운 좋은 경우였기 때문으로 보인다.  

이 버그의 무서운 점은 git을 사용하는 이유 중 하나가 완전히 뒤집힌다는 것이다.  
커밋 로그와 지속적 통합의 결합은 버그가 발생한 변경사항을 바로 찾아낼 수 있게 해 주는 강력한 결합인데, 이 경우에는 새로 커밋한 post에는 아무런 죄가 없고 기존에 잘 빌드 되던 페이지에서 에러가 발생한 것이라 오류 발생 지점을 도무지 찾을 수가 없었다. 덕분에 commit을 아무리 되돌려도 문제가 해결되지 않았다. 결국 repo에서 모든 파일을 제거했다가 하나씩 추가해 커밋하는 방식으로 무식하게 문제를 해결했다.


[jekyll-post-url-issue]:https://github.com/jekyll/jekyll/issues/3051
