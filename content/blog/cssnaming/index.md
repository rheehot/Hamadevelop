---
title: CSS 클래스에 이름을 붙여 보자! (OOCSS, BEM이란 무엇인가)
date: "2020-01-15T12:40:32.169Z"
description: 내가 클래스의 이름을 불러주기 전까지 클래스는 하나의 몸짓에 지나지 않았다.
tags: ["knowledge", "css"] 
---

![김춘수 꽃](https://pbs.twimg.com/media/BzQIu0pCIAA04OF.jpg)

>이름을 붙이는 것은 중요하다. 이름이 붙으면 의미를 가지게 된다. 심지어 원래의 의미가 있던 것도 이름이 붙으면서 다른 의미로 바뀌기도 한다. 하나의 강아지 인형에 동동이라는 이름을 붙여주면 그 인형은 단순한 인형이 아니라 나의 애완동물이 된다. 어떤 소녀에게 애칭을 주면 소녀는 나의 애인이 된다. 

프로그래밍에서도 이름을 붙이는 문제는 중요하다. 오죽하면 프로그래머가 가장 힘들어 하는 일이 이름을 짖는 것 이라는 통계 조사 결과도 있다. 

![프로그래머 고민](https://post-phinf.pstatic.net/MjAxOTAxMTFfMTMz/MDAxNTQ3MTk0ODM1NDcw.lQonZqyUQab1Log1CxIw61J1kGj7UQi7tVcgXpfBA_Eg.77jrZt4gLd-jwc4qNp-iknMnobRB67ZHGJv2rwKJDZUg.PNG/%EC%9D%BC%EC%B7%A8%ED%95%B4_HA_%282%29.png?type=w1200)
######(출처, 일 취해) 


이번 포스팅에서는 css에 이름을 붙이는 대표적인 방법에 대해서 이야기해 보고자 한다. 


CSS는 우리가 만들어 놓은 엘리먼트 들을 화면상에 배치하는 방법을 정의할 수 있는 언어다. 웹에 문서를 나타내기 위해 우리는 HTML 태그로 문서를 작성하고 태그 안에 class를 집어 넣어 CSS 스타일을 부여 한다. 

예를 들어, css 없이 아래와 같은 코드를 작성하면 화면상에 아무것도 없는 Test라는 글씨가 하나 나타날 것이다. 
```html
 <div>Test</div>
```
여기에 아래와 같이 클래스를 부여해 주고 스타일을 부여해 주면 
```html
<style>
.background-yellow{
        Background-color:yellow;
}
</style>
<div class=“background-yellow”>Test</div>
 ```
이제 Test의 배경 화면에 노란색이 칠해지는 것을 확인할 수 있다. 

이처럼 간단한 스타일을 작성하는데는 이름을 붙이는게 그렇게 어렵지는 않다. 하지만, 만약 class의 개수가 100개, 1000개를 넘어간다면 어떻게 될까? 

내가 이전에 작성한 클래스 이름과 새로운 클래스 이름이 겹치지 않는다고 확신할 수 있는가? 이전에 썼던 코드를 또 쓰고 있지는 않을까? 다른사람과 같이 작업을 한다면 그 사람의 코드와 내 코드가 겹치지는 않을까? 클래스의 이름만 보고 무엇을 위한 스타일인지 유추할 수 있을까? 

css를 조금 써보신 분들 이라면 위의 질문들에 선뜻 그렇다고 대답하기는 어려울 것이다.

그래서 몇가지 원칙을 가지고 클래스의 이름을 정하는 것이 중요하다. 일반적으로 클래스의 이름은 

- 이름을 읽으면 무슨 의미인지 알수 있돌록	
- 생김새가 아니라 어떤 목적인지 드러나게 (bigfont -> x, headerFont -> o)
- 지나치게 구체적이지 않게 
- 재사용 가능성, 유지보수를 염두에 두고 

사용하는 것을 권장한다. 하지만 이런 원칙을 가지고 있다고 하더라도 좀 뜬구름 잡는 것 처럼 느껴질 수 있다. 이러한 원칙들을 구체화 해놓은 방법론들이 있다. 

이를 CSS Naming Convention이라 한다. 가장 대표적인 방법은 OOCSS 와 BEM이 있다. (이 외에도 다양한 방법론이 있지만 전혀 모자라지 않는 [모질라 문서](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Organizing)에서 소개하는 방법이 앞의 두가지 이기에 두가지에 대해서 이야기 한다. )

###OOCSS

oocss는 Object Oriented CSS의 약자다. 객체지향 프로그래밍(링크 )의 정신을 이어 받은 것 같다. (개인적인 느낌으로는 반복되는 것을 객체화 하여 가져다 쓰는 정신을 이어받은 듯 하다.)

OOCSS 작성 원칙은 딱 두가지다. 

1. 구조와 모양의 분리
2. 콘테이너와 콘텐츠의 분리

####구조(structure)와 생김새(skin)의 분리 

파란색 버튼 스타일을 지정 싶다고 하자. 

```html
<style>
.blueButton{
	background-color: blue;
	color: white; 
	width: 20px;
	height: 20px;
}
</style>
<button class=“blueButton”>blue</button>
```

위처럼 하면 안된다는 말이다. 물론 결과는 작은파란 버튼을 보여주겠지만 OOCSS원칙에 어긋난다. 

```
<style>
.blue{
	background-color: blue;
	color: white; 
}
.button{
width: 20px;
	height: 20px;
}
</style>
<button class=“button blue”>blue</button>
```
이렇게 쓰는 것이 OOCSS원칙에 맞다. 얼핏보면 더 복잡해 보인다. 하지만 상상해 보자, 노랑버튼 빨간 버튼 회색버튼 등등등 다양한 색깔 버튼을 만들어야 한다면 우리는 그때 그때 blueButton, redButton 등등을 만들어야 할 것이다. 그 때마다 width: 20px, height: 20px; 라는 공통된 부분을 반복적으로 타이핑을 해야 할 것이다. 그리고, 버튼 크기를 바꾸고 싶을때 속성 하나 하나를 다시 타이핑 해 주어야 할 것이다. 

하지만, 이렇게 구조와 생김새를 구분하면 button이라는 클래스를 반복적으로 활용할 수 있다. 중복되는 코드를 줄일 수 있으며, 코드를 유지보수 하기에도 편하다. 그리고 blue라는 클래스도 파란색을 적용하고 싶은 엘리먼트에 반복적으로 가져다 붙일 수 있다. 

이처럼 구조와 생김새를 분리하면 중복을 없애고 재사용 가능한 CSS를 사용할 수 있다. 


#### 콘테이너와 콘텐츠의 분리 

CSS는 하위 요소 선택을 할 수 있는 문법이 있다.  예를들어 header 클래스를 가진 엘리먼트안에 있는 h1에 스타일을 적요하고 싶을 때 아래와 같은 코드를 작성할 수 있다. 
```css
.header h1{
// 스타일 적용 
}
 ```

위와같은 코드를 쓰면 header클래스를 가진 엘리먼트 안의 h1 태그에 어떠한 클래스를 부여하지 않아도 스타일을 지정할 수 있다. 

하지만 OOCSS는 이러한 선택 방법을 사용하지 않기를 권한다. 이와 같은 방법은 분명 작성하기 편리하지만, 작성시 혼란을 야기할 수 있기 때문이다. 분명 같은 h1 태그임에도 불구하고 위치에 따라 다른 모양이 된다. 이러한 방식은 작성에 혼란을 미칠 수 있다. 

문서만을 보고도 어떤 스타일이 적용 될지를 더 직관적으로 파악할 수 있는 것이 유지 보수 측면에서 더 뛰어나다. 

위의 코드를 고치려면 h1태그에 명시적으로 클래스를 지정해 주면 된다. 

OOCSS방식을 차용해서 작성하다 보면 코드의 재사용성과 명시성이 증가하는것을 느낄 수 있을 것이다. 

###BEM 

개인적으로는 OOCSS의 철학을 이해하고 응용하는 것 만으로도 충분하다고 느낀다. (아직 대규모 프로젝트에 참여한 경험이 없어서 그런 것일 수 있다.) 

하지만 프로젝트가 크고 복잡해 지고 많은 사람과 협업을 해야 할수록 더 구체적이고 누가 봐도 이해할 수 있는 이름을 작성해야 할 필요가 생길 것이다. 이럴때는 BEM을 이용하는 것이 더 좋지 않을까 생각한다. 

BEM은 Block, Element, Modifier의 앞글자를 따서 붙여진 이름이다.  BEM에서 클래스 이름을 지을 때는 Block__Element—Modifier 와 같은 모양으로 이름을 작성한다. 

Block은 홀로 존재할수 있는 하나의 단위다. 애매하지만, 뭔가 구분될수 있는 큰 구분자 라고 생각하면 좋을 듯 하다. 이를 태면 menu, header 등이 Block이 될 수 있다. 

Element는 Block안의 부속품이다. 버튼, 제목 등이 이에 해당한다. 

Modifier는 해당 Block이나 Element의 각기 다른 모양새를 말한다. 

header 클래스로 설정된 블록 안에 타이틀 엘리먼트에 파란색을 넣고 싶다면 아래 처럼 설정을 한다. 

```html
<header class=“header”>

<h1 class=“header__title header__title—blue”  > Blue Title </h1>

</header>

```

이런 식으로 이름을 정하는 것은 OOCSS보다 더 복잡해 보이지만 익숙해 지면 클래스의 이름이 더 명시적 이라는 점을 느낄 수 있다. 클래스 이름만을 읽고도 감이 확 온다. 아 헤더 아래에 있는 타이틀인데 파란색을 칠했구나..  하고 감이 확 오는 것이다. 이런 특성은 여러 사람과 함께 작업을 할때 빛이 난다. 내가 무슨의도를 가지고 작성을 했는지 전달하기 쉽다. 

또한 클래스명이 겹칠 걱정도 거의 할 필요가 없다. 헤더안에 있는 타이틀이라고 이름에서부터 명시를 하기 때문에 다른 어딘가에서 타이틀 이라는 클래스 명을 써도 헤더 타이틀에 영향을 미치지 않는다. 클래스 이름이 서로를 침범할 위험이 낮다. 

다만 개인적으로 BEM의 재사용성은 다소 떨어진다는 생각이 든다. . 블록안에서는 엘리먼트 및 컬러를 재 사용 할 수 있겠지만, 블록 밖에서는 다시 사용하기 어렵다. Menu 블록안에 header_title을 다시 쓸 수는 없다. 

명시적이고 다른 클래스의 침범을 받지 않는 BEM의 특성은 다양한 사람이 참여하는 복잡한 프로젝트에 더 적합할 것이라고 생각한다. 

사실 최신 css 트랜드는 CSS-in-JS 스타일이다. 이 방식은 특정 컴포넌트와 CSS를 하나로 묶어서 네이밍에 고려해야할 부분을 대폭 축소 시켰다. 이에 대해서는 다음에 기회가 될때 설명해 보도록 하겠다. 