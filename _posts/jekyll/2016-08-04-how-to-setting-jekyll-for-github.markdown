---
layout: post
title:  "어떻게 Jekyll을 이용해서 github 페이지를 구성하는가?"
date:   2016-08-04 09:35:00 +0900
categories: Jekyll
tags : jekyll
---
Github의 무료 호스팅 서비스는 블로그를 만들기에 아주 좋다.

예전부터 이용하고는 있었는데 블로그로 사용하기에는 jekyll이 좋다는 소문을 듣고 시도해보는 중이다.

의외로 [Github 공식 도움말][github-jekyll-docs] 처럼 자세히 설명된 문서를 보면서 한 단계씩 따라하면 세팅은 어렵지 않다. 찾아보면 jekyll을 설치하고 Github에서 사용하는 방법이 여러가지가 있는데 반드시 자신이 어떤 세팅을 사용했는지 기억해두자. 나중에 원격 저장소에는 소스만 덜렁 있고 정작 어떤 환경에서 실행했는지 까먹어서 진땀 빼는 경우가 생긴다. 내 경우 윈도우즈 10 에서 만들어 놓은 저장소를 OS X로 옮기면서 구글링을 꽤 해야 했다. 설치법을 어디에 적어두는 것이 제일 좋다.

취향에 따라 Grunt 대신 Gulp를 쓰기도 하고 패키지 매니저도 운영체제나 취향에 따라 Homebrew를 통해 설치하거나 npm을 통해 설치하는 등 다양한 변수가 존재하는데 웬만하면 했던 대로 다시 하는게 좋다. A방법으로 설정한 프로젝트를 다시 B환경에서 실행하려고 하면 버전 이슈나 패키지 충돌 등이 발생할 가능성이 높다. 나는 윈도우에서 루비 인스톨러를 이용해 루비를 설치하고 환경을 잡았는데 나중에 OS X에서는 홈브류로 관련 패키지를 설치하면서 루비를 재설치했다가 루비 버전 충돌 이슈에 한참 삽질했다. rvm을 설치하고 나서야 해결되었다. [비슷한 이슈로 고통받는 글][stackoverflow-error-jekyll]

기본적으로 Github 도움말을 참조해서 설정을 잡았는데, [Github 공식 도움말][github-jekyll-docs]에서는 Ruby Bundler를 설치하고 Bundler를 통해서 jekyll을 설치하는 식으로 되어 있다. 이 방법을 추천한다. 내 경우 다른 패키지 의존성은 bundler가 처리해줘서 Ruby 버전 충돌만 해결하니까 OS X에서도 jekyll이 제대로 구동되었다. 대신 jekyll을 실행할 때 잊지말고 bundle exec jekyll 하는 식으로 bundle을 통해야 한다. 안그러면 의존성 지옥을 보게 될 것이다.

Github 도움말 다음으로 가장 많이 보게 될 사이트는 아마도 [jekyll 문서 번역본][jekyll-docs-korean]이다.
jekyll 자체에 대한 이해가 없으면 블로그 구성이 꽤 성가셔진다. 마크업 언어 모르는 상태로 깃허브 위키 페이지 만드는 정도로 성가시다.

그리고 놓치기 쉬운 팁이지만 \_config.yml 파일에 보면 baseurl: "" 부분이 있다.
이 부분을 Github세팅에 맞춰주지 않으면 정작 Github에서 호스팅되는 페이지가 이상해진다. 에러를 뜯어보면 css등 필요 파일의 경로를 찾지 못하는 것을 볼 수 있다. 로컬에서 잘 나왔다고 방심하지 말자. 참고로 이 문제는 유저 페이지인 경우에는 발생하지 않는다. Github에서 페이지를 호스팅해주는 방식은 2가지가 있는데 유저 페이지의 경우는 baseurl이 공백인 것과 같기 때문에 상관없고, 저장소에 대한 호스팅의 경우에 문제가 생긴다. 예를 들어 이 프로젝트는 `blog` 프로젝트이므로 호스팅 경로가 아이디.github.io`/blog`/ 하는 식으로 나타나는데, 이때 baseurl:"/blog" 설정을 해 줘야 의도한 대로 페이지가 나타난다. 로컬에서는 그냥 localhost:4000으로 돌리기 때문에 baseurl이 공백이라 이 문제를 만나지 못했던 것 뿐이다.
그런데 baseurl을 설정해주고 나면 이제는 localhost:4000에서 Github 프로젝트 구성과 설정이 안 맞게 되어 로컬에서 페이지를 확인할 수가 없게 된다. 이때도 아주 쉽게 해결할 수 있는데(난 몰라서 오래 삽질했다)

`bundle exec jekyll serve --watch --baseurl ''`

이렇게 해 주면 baseurl이 공백으로 설정된 상태로 로컬 jekyll 서버가 실행된다.

참고로 옵션 `--watch`는 프로젝트 디렉토리 내부의 파일이 변경될 경우에 jekyll에서 알아서 서버를 업데이트해주는 옵션으로 테스트할때 아주 유용하다. 포스팅 내용을 변경하며 서버를 내렸다 올리지 않아도 블로그 내용이 알아서 변경된다.
그렇다고 만능은 아니라 \_config.yml같이 심각한 변경사항은 서버 내렸다 올려야 반영된다.

지금 이 블로그 페이지는 jekyll 기본 테마인데 이걸 뜯어고치는 주제로 포스팅을 더 진행해볼까 생각 중이다.

[jekyll-docs-korean]: https://jekyllrb-ko.github.io/
[github-jekyll-docs]: https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/
[stackoverflow-error-jekyll]: http://stackoverflow.com/questions/38677296/error-running-jekyll-on-ubuntu-14-04
