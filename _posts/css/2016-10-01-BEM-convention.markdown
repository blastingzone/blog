---
layout: post
title:  "BEM : Block, Element, Modifier"
date:   2016-10-02 04:15:00 +0900
categories: css
tags : css
---
### BEM

[Get Bem][bem-link]

자세히 알고 싶다면 위 사이트를 방문해보자.

BEM은 CSS 작성 규칙 중 하나다.  
반드시 이렇게 해야 한다는 것은 아니지만 생각없이 CSS를 짜다보면 상당히 위험한 구조의 셀렉터를 남발하게 되면서 코드가 아주 개판이 되는 경우가 많은데 BEM 또한 어떻게 하면 CSS를 좀 더 쓸만하게 작성할 수 있을까를 고민한 결과라고 볼 수 있다. 실제로 써먹기에도 나쁘지 않다.

한 가지 반드시 명심해두면 좋을 실전적인 팁은 BEM을 도입하도라도 재사용성을 높이기 위해서는 페이지 디자인 자체가 Component 기반으로 움직여여야 한다는 것이다. 비슷한 구조를 가진 것 같아도 여기저기 조금씩 다른 디자인으로 구성된 페이지는 결국 Modifier가 줄줄이 붙게 되면서 생각만큼 BEM 컨벤션을 도입한 효과를 볼 수 없게 된다.  

뻔한 소리지만 그냥 방법론을 도입하는데서 그치지 말고 사내문화가 되도록 해야 한다는 이야기.

### Block? Element? Modifier?

Block은 가장 큰 단위로 독립적으로 사용할 수 있고 그 자체로 의미를 가진 요소를 뜻한다.  
예컨대 화면 상단에 노출되는 <header>같은 것이 Block 요소다.

Element는 block의 부분을 이루는 요소인데 화면 상단 바에 들어있는 메뉴들이 Element에 해당한다.

Modifier는 block이나 Element의 변형으로, 만약 <header>에 들어있는 메뉴 중에 첫 번째인 메뉴는 font도 더 크고 클릭하면 index 페이지로 넘어가야 한다는 요구조건이 있다고 생각해보자. 이런 경우 Element 이름 뒤에 Modifier를 붙여서 클래스명을 지을 수 있다.

이 큰 틀을 잊어버리지 않으면 개발팀 내부에서 위 개념을 응용한 별도의 컨벤션을 사용하여도 무방할 것이다. 대체로 block-name__element-name--modifier-name 같은 식의 명명 규칙을 쓴다.

[bem-link]:http://getbem.com/
