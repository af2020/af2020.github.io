---
author: admin
comments: true
date: 2011-04-16 05:12:20+00:00
layout: post
link: http://hubnode.cafe24.com/wp/archives/1387
slug: '%ed%81%ac%eb%a1%ac-%ed%99%95%ec%9e%a5%ed%94%84%eb%a1%9c%ea%b7%b8%eb%9e%a8-ireader-%ec%84%9c%ec%b2%b4-%eb%b3%80%ea%b2%bd'
title: 크롬 확장프로그램 iReader 서체 변경.
wordpress_id: 1387
categories:
- IT
---

사파리에서 선보인 "읽기도구"는 지저분한 광고를 없애고 원문만을 그대로 보여주어 글읽기 자체에 집중할 수 있게 해주는 매력적인 도구이다. 그런데, 초기 설정되어 있는 서체나 줄간격이 한글을 잘 읽기에는 2% 부족한 느낌이다. [많은 분들이 이 점에 공감](http://www.google.co.kr/search?aq=f&sourceid=chrome&ie=UTF-8&q=%EC%82%AC%ED%8C%8C%EB%A6%AC+%EC%9D%BD%EA%B8%B0%EB%8F%84%EA%B5%AC+%ED%81%AC%EB%A1%AC#sclient=psy&hl=ko&newwindow=1&source=hp&q=%EC%82%AC%ED%8C%8C%EB%A6%AC+%EC%9D%BD%EA%B8%B0%EB%8F%84%EA%B5%AC+%EC%84%9C%EC%B2%B4&aq=f&aqi=&aql=&oq=&pbx=1&fp=32c87d334e8598e)하고 있었고, 변경할 수 있는 방법이 있었다. [사파리가 설치되어 있는 폴더의 "reader.html" 파일의 내용을 수정](http://left.tistory.com/entry/%EC%82%AC%ED%8C%8C%EB%A6%AC5%EC%9D%98-%EC%9D%BD%EA%B8%B0%EB%8F%84%EA%B5%AC-%EC%84%9C%EC%B2%B4%EB%B3%80%EA%B2%BD%ED%95%98%EA%B8%B0)하여 사용자 입맛에 맞게 바꿀 수 있다.

이와 유사한 기능을 하는 [크롬용 확장프로그램이 iReader](https://chrome.google.com/extensions/detail/ppelffpjgkifjfgnbaaldcehkpajlmbc?hl=ko) 이다.

작동되는 방식은 유사하다. 주소창 오른쪽 끝부분에 생긴 아이콘을 클릭하면 원문만 추려서 깔끔하게 보여준다. 그런데, 여기도 같은 문제가 있다. 서체랑 줄간격이 마음에 들지 않는다. iReader는 옵션에서 서체 변경을 할 수 있게 지원하고 있다. 그런데, 영문서체만 제공되어 비영어권 사용자는 불편을 느낀다. 실제로[ iReader 개발 사이트 Issue Tracker를 살펴보면](http://code.google.com/p/ireader-extension/issues/list?can=2&q=font&colspec=ID+Type+Status+Stars+Mstone+Summary+Reporter&cells=tiles), 비영어권 사용자의 서체 추가 및 변경에 대한 요구가 적지 않게 올라와 있다.

그래서, 직접 바꿔봤다.
크롬 확장 프로그램들이 모여 있는 폴더에서 사파리의 reader.html 파일과 같은 역할을 하는 파일을 찾았다. 바로 아래의 폴더에 있던 reader.html 파일이었다. 크롬의 버전에 따라서 끝부분 폴더구조는 다를 수 있다. Extensions 아래 서브 폴더명들이 다들 이런식이어서 구분이 어렵다. Extensions 폴더에서 reader.html 파일을 검색하여 찾았다.




<blockquote>
c:\Users\[User ID]\AppData\Local\Google\Chrome\User Data\Default\Extensions\ppelffpjgkifjfgnbaaldcehkpajlmbc\1.3.0.2_0\
</blockquote>



파일 편집 프로그램으로 이 파일을 열어서, ".page" 부분에 "맑은 고딕" 폰트를 추가하고, 줄 간격을 조금 높였다. 개인적으로 눈이 편안한 회색 배경을 좋아하는데, background color 부분의 RGB code를 바꿔주면 된다.




<blockquote>
.page {
	?display: inline-block;
	font: 19px **"Malgun Gothic"**,Georgia, Times, "Times New Roman", serif;
	border: 1px solid #C3C3C3;
	**line-height: 180%;**
	**background-color: #dddddd;**
	?padding: 45px 70px;
	margin: 12px 12px 0px 23px;
	-webkit-user-select: auto;
	/*-webkit-box-shadow: rgba(0, 0, 0, 0.4) 0px 0px 40px;*/
		}
</blockquote>



수정하여 저장한 후, 크롬을 다시 실행하면 적용이 된다. 적용을 하기 전과 한 후의 읽기 창 모습은 아래와 같다.

적용 전




<blockquote>
[![font_b.jpg](http://lh5.ggpht.com/_F9iY7Q3PUXc/TakggIYHyZI/AAAAAAAAB9M/iJPaAEB1XHo/s150-c/font_b.jpg)](http://lh5.ggpht.com/_F9iY7Q3PUXc/TakggIYHyZI/AAAAAAAAB9M/iJPaAEB1XHo/font_b.jpg) 
<table ></table>
</blockquote>



적용 후




<blockquote>
[![font_a2.jpg](http://lh6.ggpht.com/_F9iY7Q3PUXc/TaknsOU8gyI/AAAAAAAAB9Y/TUIPvsI_94M/s150-c/font_a2.jpg)](http://lh6.ggpht.com/_F9iY7Q3PUXc/TaknsOU8gyI/AAAAAAAAB9Y/TUIPvsI_94M/font_a2.jpg) 
<table ></table>
</blockquote>



덕분에 글 읽기가 한층 쾌적해졌다.~

P.S. iReader에서 제공하는 옵션에는 어떤 방식으로 적용되는지도 궁금하다. iReader 옵션 창에서 사용자 지정 서체가 보여질 수 있으면 좋겠는데 그건 잘 안되었다. 위의 확장 프로그램 폴더에 보면, option.html 파일이 있는데, 거기게 폰트를 추가하면 콤보박스에서는 보이는데, 테스트해보니 작동이 잘 되지는 않았다. 아직 내공 부족! 











