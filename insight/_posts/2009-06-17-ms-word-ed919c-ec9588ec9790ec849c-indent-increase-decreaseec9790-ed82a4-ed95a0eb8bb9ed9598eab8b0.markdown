---
author: neo
comments: true
date: 2009-06-17 13:20:12+00:00
layout: post
link: http://hubnode.cafe24.com/wp/archives/172
slug: ms-word-%ed%91%9c-%ec%95%88%ec%97%90%ec%84%9c-indent-increase-decrease%ec%97%90-%ed%82%a4-%ed%95%a0%eb%8b%b9%ed%95%98%ea%b8%b0
title: MS Word 표 안에서 Indent Increase에 Hot Key 할당하기
wordpress_id: 172
categories:
- IT
---

MS Word는 글머리 설정을 할 경우, Enter키를 칠 때, 다음 줄에서 글머리를 자동으로 붙여준다.
이때, Tab 키를 치면 Indent Increase (들여쓰기 하위 수준으로 이동)가 된다.

그런데, 표를 만들고 표 안에서 위의 기능을 쓰려고, Tab 키를 치면, Indent Increase가 안되고, 다음 셀로 이동해 버린다.
표 안에서 여러 줄에 걸쳐 글머리 기호와 함께 글을 쓸 경우에는 은근히 신경쓰이는 불편한 부분이다.

해당 명령에 키보드 Hot Key를 할당하면 이런 불편을 조금 덜 수 있는 것 같다.

2003 버전 기준이다.

Step 1. 보기 >> 도구모음 >> 사용자 지정
Step 2. 아래쪽 "키보드" 버튼 클릭!
![](http://hubnode.cafe24.com/wp/wp-content/uploads/2009/06/cap_298.jpg)

Step 3. "키보드 사용자 지정" 대화상자에서 아래와 같이 설정.
            명령지정 영역. 범주:서식, 명령: IncreaseIndent
            키보드시퀀스지정영역. '새바로가기키'에 커서를 두고 바로가기키 설정

![](http://hubnode.cafe24.com/wp/wp-content/uploads/2009/06/cap_299.jpg)

이렇게 하면, 표 안에서 설정한 핫키로 Increase Indent를 할 수 있게 된다.
상위수준으로 올라가는 것은... Decrease Indent 이고, 명령에도 있기 때문에 마찬가지 요령으로 설정하면 된다.
