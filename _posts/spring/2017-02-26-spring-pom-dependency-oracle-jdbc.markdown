---
layout: post
title:  "Spring에서 Maven Repository를 통해 Oracle JDBC를 불러오려구요?"
date:   2017-02-26 16:35:00 +0900
categories: spring
tags: spring oracle
---
### 결론

Maven Repository에 더 이상 Oracle JDBC는 존재하지 않기 때문에 Oracle 홈페이지에서 직접 다운받아서 프로젝트에 포함시켜야 한다.

또는 [이 글][get-oracle-jdbc]에서 시키는 대로 별도의 유저 인증과 설정이 필요하다.

### 삽질

구글링을 통해 Oracle DB와 Spring을 연결하는 튜토리얼을 찾아서 따라하는 중이었다.  
그런데 시키는 대로 해도 Oracle JDBC를 불러올 수가 없었다.  

대체 왜?

Maven 에러가 계속 발생해서 원인을 찾아보니 더 이상 public Maven Repository에 Oracle JDBC가 지원되지 않는다는 것이다.

결국 Oracle 홈페이지에서 직접 JDBC를 다운받아서 프로젝트에 포함시켜 문제를 해결했다.

### 방법이 없진 않다

나중에 더 조사해 본 결과 [사용자 인증을 통해 Maven Repository에서 Oracle JDBC를 사용][get-oracle-jdbc]하는 방법이 존재하는 것을 확인하였다.

[get-oracle-jdbc]:https://blogs.oracle.com/dev2dev/get-oracle-jdbc-drivers-and-ucp-from-oracle-maven-repository-without-ides
