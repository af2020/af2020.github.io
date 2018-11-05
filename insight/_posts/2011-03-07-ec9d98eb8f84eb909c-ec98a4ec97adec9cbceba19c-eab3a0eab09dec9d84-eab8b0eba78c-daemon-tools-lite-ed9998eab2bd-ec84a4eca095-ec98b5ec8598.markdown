---
author: admin
comments: true
date: 2011-03-07 14:25:01+00:00
layout: post
link: http://hubnode.cafe24.com/wp/archives/1362
slug: '%ec%9d%98%eb%8f%84%eb%90%9c-%ec%98%a4%ec%97%ad%ec%9c%bc%eb%a1%9c-%ea%b3%a0%ea%b0%9d%ec%9d%84-%ea%b8%b0%eb%a7%8c-daemon-tools-lite-%ed%99%98%ea%b2%bd-%ec%84%a4%ec%a0%95-%ec%98%b5%ec%85%98'
title: '의도된 오역으로 고객을 기만: ''DAEMON Tools Lite'' 환경설정 옵션.'
wordpress_id: 1362
categories:
- IT
---

어제 [DAEMON Tools Lite](http://www.daemon-tools.cc/kor/products/dtLite)를 설치하고 사용하다 오늘 겪은 일이다.

이 프로그램은 대체로 프로그램을 설치할 때에만 필요하기 때문에 윈도우 시작시에 이 프로그램이 자동으로 실행되도록 할 필요는 없다. 프로그램을 새로 설치하려고 할 때 수동으로 실행하면 되기 때문이다. 물론 가상 CD를 자주 사용하기 때문에 이 기능이 꼭 필요할 수도 있겠지만, 나는 그런 경우는 아니어서 윈도 시작시에 자동으로 실행되는 옵션을 끄고 싶었다.

그래서 환경설정 옵션을 살펴보았다. 꼭 있어야 할 옵션이기 때문에 첫 화면에 바로 보이지 않을까 하는 기대가 있었다. 첫 화면이 아래와 같았다.

[![cap_001.jpg](http://lh5.ggpht.com/_F9iY7Q3PUXc/TXTbqvDmEQI/AAAAAAAAB8g/JEwN6z2h30M/s150-c/cap_001.jpg)](http://lh5.ggpht.com/_F9iY7Q3PUXc/TXTbqvDmEQI/AAAAAAAAB8g/JEwN6z2h30M/cap_001.jpg) <table ></table>

어쭈구리.. "윈도우 시작시에 자동으로 실행"과 같은 옵션이 있을 줄 알았는데 없다. 환경설정 메뉴의 여기 저기를 한참 뒤지고 다녔다.

그야말로 한참 뒤에 첫 화면 맨 위에 있는 "**DTPro 에이전트 사용**" 이라는 무슨 기능인지조차 알기 어려운 이 옵션의 **툴팁**이 "**시스템 시작시 DAEMON Tools Lite 자동으로 시작**" 이라는 것을 알게 되었다. 아래 그림을 살펴보자. 

[![cap_002.jpg](http://lh6.ggpht.com/_F9iY7Q3PUXc/TXTbqkKDgmI/AAAAAAAAB8c/VUGks_I7tNA/s150-c/cap_002.jpg)](http://lh6.ggpht.com/_F9iY7Q3PUXc/TXTbqkKDgmI/AAAAAAAAB8c/VUGks_I7tNA/cap_002.jpg) <table ></table>

여기서 의문이 든다.
"DTPro 에이전트 사용" 이 "시스템 시작시 DAEMON Tools Lite 자동으로 시작" 이라구?
영문 번역이 잘못되었기 때문이 아닐까?
의역이 아닌 직역을 했기 때문이라고 생각하여 아래와 같이 언어를 영문으로 바꿔보았다.

[![cap_004.jpg](http://lh4.ggpht.com/_F9iY7Q3PUXc/TXTfAEFPmUI/AAAAAAAAB8o/5ZMjXYdliRk/s150-c/cap_004.jpg)](http://lh4.ggpht.com/_F9iY7Q3PUXc/TXTfAEFPmUI/AAAAAAAAB8o/5ZMjXYdliRk/cap_004.jpg) <table ></table>

"Use Tray Agent".
그 이상한 한글 번역보다 이 영문이 훨씬 직관적이다. 
왜 이 영문 문구가 "DTPro 에이전트 사용" 이라는 이상한 한글 문구로 번역 되어 있을까?
"Tray"라는 자주 쓰는 용어는 오히려 없애고, "Agent"라는 모호한 용어를 "에이전트"라고 한글로 바꾸었다. 물론 영문 툴팁의 경우에도 "Launch DAEMON Tools Lite automatically on system start up" 이라는 쉬운 용어로 되어 있다.

"DTPro 에이전트 사용" 이라는 문구를 보고 무슨 기능을 하는 옵션인지 한번에 알 수 있는 한국인은 많지 않을 것이다.
하지만, "시스템 시작시 DAEMON Tools Lite 자동으로 시작"이라는 문구가 무엇을 의미하는 지는 훨씬 많은 사람이 이해할 수 있을 것이라고 생각한다. 

번역자가 이런 사실을 모르진 않았을 것이다. 툴팁은 매우 정확하게 표시되어 있지 않은가.
물론 영문의 경우에도 "Use Tray Agent" 보다는 "Launch DAEMON Tools Lite automatically on system start up" 라는 문구가 훨씬 직관적이다.

왜 이렇게 하였을까?

사용자들은 대체로 "**이해하기 어려운 옵션은 Default로 두는 경향**"이 있다. 알기 어려운 옵션을 건드려 문제를 발생시키고 싶지 않기 때문이다. 눈에 보이는 "메뉴명"에 일일이 마우스를 오버하여 "툴팁"을  확인해보는 사람도 많지 않을 것이다.

이는** Default 옵션의 체크가 풀리는 것을 조금이라도 막아보려는 "의도적인 오역"이 분명하다.** 사실 한참을 찾아 헤메다 옵션 해제를 포기하기 직전에 저 툴팁을 발견하였다. 찾기를 포기한 대부분의 사용자는 거의 사용하지 않는 "DAEMON Tools Lite"를 어쩔 수 없이 시스템 시작시마다 자동으로 실행해야 할 것이다. 이런 기능 자체를 잘 모르는 사용자야 어쩔 수 없다고 해도 이 기능을 사용하고 싶지 않은 사용자도 "**옵션 해제 방법을 찾다가 지치게 만들어**" 자포자기 상태로 계속 사용하도록 하기 위한 의도가 있는 것이다.

"직관적인 문구는 너무 길기 때문에 미관상 단축하기 위해서"라고 말할 수 있을 것이다. 그렇다면 "DTPro 에이전트 사용"보다는 "시스템 시작시 자동 실행"이라는 문구 였어야 했다. "무지"에 의한 것이 아니라면 "의도적인 오역"의 혐의를 벗기 어렵다.

내 시스템 자원을 몰래 도둑질하려는 것이라는 생각이 들어 불쾌했다.

S/W 사용 빈도를 높이려는 욕심이 있다면 정공법으로 가야 한다. 


