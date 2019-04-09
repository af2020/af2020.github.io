---
author: neo
comments: true
date: 2010-11-03 12:17:38+00:00
layout: post
link: http://hubnode.cafe24.com/wp/archives/749
slug: '%ec%98%b5%ed%8b%b0%eb%a8%b8%ec%8a%a4%ed%81%90-%ed%82%a4%eb%b3%b4%eb%93%9c-%eb%b0%8f-%eb%b2%84%ed%8a%bc-%ec%84%b8%ed%8c%85'
title: 옵티머스큐 키보드 및 버튼 세팅
wordpress_id: 749
---

지난 주말에 작업한 옵티머스 큐(LG-LU2300) 키보드 세팅 내용을 정리해두려고 한다.
첫째는 폰이 고장나서 다시 세팅해야 할 경우를 대비해서이고, 둘째는 옵큐를 갖고 있는 분들과 공유하고 싶어서다.

소스는 네이버 카페 ([http://cafe.naver.com/bjphone](http://cafe.naver.com/bjphone)) 에서 얻었다.

먼저 옵티머스 큐 키보드 모습이다. (사진 클릭하면 확대, 사진출처: [http://bit.ly/davGK0](http://bit.ly/davGK0))

<!-- more -->


<blockquote>
[![cap_003.jpg](http://lh4.ggpht.com/_F9iY7Q3PUXc/TNE9rEaOonI/AAAAAAAABYY/a029EklgPWM/s288/cap_003.jpg)](http://lh4.ggpht.com/_F9iY7Q3PUXc/TNE9rEaOonI/AAAAAAAABYY/a029EklgPWM/cap_003.jpg?imgmax=800)
</blockquote>




옵티머스큐는 키보드는 감이 좋다.
그러나, 키보드를 구성하신 분은 분명히 스마트폰에 키보드를 장착하여 실제 사용해본 경험이 많은 분이 아니라는 생각이 든다.

옵티머스 큐 키보드의 문제점은 아래와 같다. 나 뿐만 아니라 이 폰을 사용하는 분들의 공통적인 생각이다.




<blockquote>
1. 왼쪽 SHIFT 키가 있는데, 오른쪽에는 없다. 대신 엔터키가 그 자리에 있다. 엔터키는 방향키 가운데 키로 충족된다. 엔터키 자리에는 마땅히 오른쪽 SHIFT키가 와야 한다.

2. 일반 키보드의 CTRL 키랑 비슷한(?) 역할을 하는 일명 파란색키(키보드에 파란색으로 표시된 글자 및 기호 입력시 사용)도 왼쪽에만 있다. 오른쪽에 있는 검색키는 별로 쓸일이 없다. 이 자리에 왼쪽에 있는 키와 같은 역할을 하는 파란색키가 있어야 한다.

3. 복사, 붙여넣기, 자르기 등에 사용되는 메뉴키가 그 키와 함께 눌러야 하는 키들(C, V, X) 근처에 있다. 왼손가락으로 메뉴키를 누른 상태에서 C, V, X 키를 누르려면 손가락이 꼬이게 된다. 실제 하려고 들면 누를 수도 없고, 매우 우스꽝스런 상황이 된다.

4. 파란색키가 할당되어 있지 않은 Q, W, E, R, T, Y, P 키가 아깝다. 파란색키에 할당된 기호 중에 자주 사용하는 ", =, +, - 같은 것이 없다. [,] 같이 정말 자주 쓰는 대괄호도 없다. 탭키도 없다. 이런 키를 입력하려면 메뉴를 한참타고 들어가야 하는데, 그러면 터치입력에 비한 쿼티폰의 장점이 반감되는 것이다.

5. 키보드 슬라이드를 열게 되면, 사진버튼 누르는 것이 매우 불편하다. 지식사전을 실제로는 잘 쓰지 않으니, 그 자리에 사진 버튼이 있어야 한다. 지식사전 어플은 화면 터치로 실행해도 충분하다.

6. 전원 키 위치가 매우 불편한 곳에 있어 누르기 어렵다. 한편 핸드폰 한 가운데 아래에 있는 검색 버튼은 어플 터치하는 것으로 충분히 가능하다. 화면 켜고 끄는 기능을 이 검색키에 할당하면 전원키의 불편함을 해소할 수 있다.

</blockquote>



어쨋거나, 이런걸 개선하기 위해 키배열을 바꾸거나, 새로운 키를 추가하였다.

이 작업을 하려면 안드로이드 OS에 대한 루트 권한을 획득(루팅)해서 파일을 수정해야 한다.
폰이 출시될 때에는 일반 사용자 권한으로 출시되기 때문에 루팅을 위한 과정이 필요하다.

루팅되었다는 전제를 한다.
파일 브라우징은 루트탐색기, 폰에서의 파일 편집은 Text Editor를, PC에서의 파일 편집은 Ultra Editor를 이용하였다.



<blockquote>
I. 1~4번 작업은  "/system/usr/keylayout/pp2106_qwerty.kl" 파일을 폰에서 직접 수정하였다.

II. 5번 작업은 "/system/usr/keychars/pp2106_qwerty.kcm.bin" 파일을 PC로 가져와 파일 에디터로 수정한 후 폰에 적용하였다.

III. 6번 작업은 "/system/usr/keylayout/surf_keypad.kl"  파일을 폰에서 직접 수정하였다.

</blockquote>


============================
I. 루트 탐색키로 "/system/usr/keylayout/pp2106_qwerty.kl" 이 파일을 찾아서 손가락으로 꾹~ 누르면 뜨는 컨텍스트 메뉴 맨 아래에 "텍스트 편집기로 열기"가 있다. 파일을 열고 아래와 같이 폰에서 수정한다.
============================


<blockquote>
1. 엔터키로 할당된 키에 오른쪽 SHIFT 키를 할당한다.

key 28 ENTER WAKE_DROPPED
==> key 28 SHIFT_RIGHT WAKE_DROPPED

2. 검색키로 할당된 키에 오른쪽 파란색키를 할당한다.

Key 217 SEARCH WAKE_DROPPED 를
==> Key 217 ALT_RIGHT WAKE_DROPPED

3. 왼쪽 메뉴키와 오른쪽 기호키를 교환한다.

Key 139 MENU   WAKE_DROPPED
==> Key 139 SYM_POP   WAKE_DROPPED

Key 61 SYM_POP   WAKE_DROPPED
==> Key 61 MENU   WAKE_DROPPED

4. 지식사전 버튼에 카메라키 할당한다.

key 251 EDIC WAKE_DROPPED
==> key 251 CAMERA

</blockquote>




파일을 수정하면 아래와 같다.(사진 클릭 확대) 만약을 위해서 원래 파일앞에 #을 추가하는 것이 안전하니 참고...





<blockquote>
[![C2010-11-03 20.35.27.jpg](http://lh6.ggpht.com/_F9iY7Q3PUXc/TNFOPVULV7I/AAAAAAAABZQ/HpejV65_sEI/s288/C2010-11-03%2020.35.27.jpg)](http://lh6.ggpht.com/_F9iY7Q3PUXc/TNFOPVULV7I/AAAAAAAABZQ/HpejV65_sEI/C2010-11-03%2020.35.27.jpg?imgmax=800)

[![C2010-11-03 20.53.06.jpg](http://lh4.ggpht.com/_F9iY7Q3PUXc/TNFOPpmQrJI/AAAAAAAABZU/JlAB_2dcBnk/s288/C2010-11-03%2020.53.06.jpg)](http://lh4.ggpht.com/_F9iY7Q3PUXc/TNFOPpmQrJI/AAAAAAAABZU/JlAB_2dcBnk/C2010-11-03%2020.53.06.jpg?imgmax=800)
</blockquote>



============================
II. 루트 탐색키로 "/system/usr/keychars/pp2106_qwerty.kcm.bin" 이 파일을 찾아서 손가락으로 꾹~ 누르면 뜨는 컨텍스트 메뉴 중에서 "보내기" 메뉴를 선택하면 폰에 설치되어 있는 어플 종류에 따라서 보내기 할 다양한 어플을 선택할 수 있다. 파일을 PC로 가져오는 방법은 생략한다.
============================

우선 Q,W,E,R,T,Y,P 키에 어떤 키를 할당한지를 결정해두어야 한다. 엑셀에서의 간단한 계산을 위해 =, +, - 를, 문서작업시 대괄호([ ])를 자주 사용하는 습관이 있어서 이 키를 또 쌍따옴표(")를 할당하고 싶었고, 탭키를 할당했다. 정리하면 아래와 같다.




<blockquote>
Q ==> =
W ==>+
E ==> -
R ==> [
T ==> ]
Y ==> "
P ==> Tab
</blockquote>




Ultra Editor로 파일을 열어보면 아래와 같이 수정하였다. (사진 클릭 확대)
붉은색 네모로 표시된 부분이 수정된 부분이다. 점과 점사이에 위에서 결정한 할당하기 원하는 기호들을 넣었다.
Tab 키의 경우 왼쪽에서 직접 코드값을 써주는 방식으로 수정했다.




<blockquote>
[![cap_005.jpg](http://lh3.ggpht.com/_F9iY7Q3PUXc/TNFZyOr5nyI/AAAAAAAABZg/ylCo6ZwTCpU/s288/cap_005.jpg)](http://lh3.ggpht.com/_F9iY7Q3PUXc/TNFZyOr5nyI/AAAAAAAABZg/ylCo6ZwTCpU/cap_005.jpg?imgmax=800)
</blockquote>



============================
III. 루트탐색기로 "/system/usr/keylayout/surf_keypad.kl" 파일을 열어서 손가락으로 꾹~ 누르면 뜨는 컨텍스트 메뉴 맨 아래에 "텍스트 편집기로 열기"가 있다. 파일을 열고 아래와 같이 폰에서 수정한다.
============================



<blockquote>
key 217 SEARCH WAKE_DROPPED
==> key 217 ENDCALL WAKE
</blockquote>



파일을 수정하면 아래와 같다.



<blockquote>
[![C2010-11-03 21.52.10.jpg](http://lh6.ggpht.com/_F9iY7Q3PUXc/TNFb2P80w5I/AAAAAAAABaA/9fJly3NCMfk/s288/C2010-11-03%2021.52.10.jpg)](http://lh6.ggpht.com/_F9iY7Q3PUXc/TNFb2P80w5I/AAAAAAAABaA/9fJly3NCMfk/C2010-11-03%2021.52.10.jpg?imgmax=800)
</blockquote>



이렇게 세팅한 다음 오래 쓰지는 않았기 때문에 불편한 점이 발견되어 또 변경할 수도 있을 것 같다.
현재까지는 기본 세팅보다는 훨씬 좋다.


Reference page.


<blockquote>
1. [http://bit.ly/dtSFcv](http://bit.ly/dtSFcv)
2. [http://bit.ly/dzu7zL](http://bit.ly/dzu7zL)
3. [http://bit.ly/dxXJ9W](http://bit.ly/dxXJ9W)
4. [http://bit.ly/atKA8h](http://bit.ly/atKA8h)
5. [http://bit.ly/a5CZHE](http://bit.ly/a5CZHE)
6. [http://insjang.tistory.com/](http://insjang.tistory.com/)
</blockquote>
