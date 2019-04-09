---
author: neo
comments: true
date: 2009-12-10 04:19:14+00:00
layout: post
link: http://hubnode.cafe24.com/wp/archives/532
slug: picasa%eb%a5%bc-%ed%86%b5%ed%95%9c-%ec%82%ac%ec%a7%84-%ea%b4%80%eb%a6%ac-%ec%8b%9c%ec%9e%91
title: Picasa를 통한 사진 관리 시작.
wordpress_id: 532
---

필카에서 디카로 넘어오면서, 공간을 차지하는 필름과 인화물을 벗어나, 컴퓨터를 이용해서 사진 파일들을 체계적으로 관리할 수 있을 것이라고 막연하게 기대했었다. 웬걸, 필카 때와는 비교할 수 없을 만큼 늘어나는 사진의 양을 감당하기 어려웠다. 최근에 뭔가 해결방안을 찾지 않으면 안되겠다고 느낀 건, 노트북 저장공간의 대부분이 사진 파일들로 차버려서 긴급조치를 강요받았기 때문이다. 늘 이렇게 벼랑에 내몰려야 팔 걷고 달려들게 된다.

사진파일 관리에 대한 문제 의식은 이런 것들이다.



<blockquote>
1. 사진이 계속 늘어날 것이고, 그 속도는 더 빨라질 것이다. 저장공간은 제한되어 있는데, 사진만으로 하드를 채우기는 싫다.
2. 그렇게 많은 사진을 저장해둬도 실제 잘 보게 되지 않는다. 인화도 잘 안하게 되고, 앨범에 넣어놔도 잘 안보게 된다.
3. 아이들 사진을 찍다보니, 가족들과 나누고 싶다.
4. 블로그 호스팅 공간, 트래픽 이런 것도 생각된다. 외부 서비스에 사진을 올려두고, 블로그에서 링크로 보여주고 싶다.
5. 가능하면 무료나 매우 싸게 웹 공간을 제공 받아서 사진 관리까지 같이 하면서 블로그 사진 링크로 이용하고 싶다.
</blockquote>



사진을 많이 찍는 분이라면 누구나 이런 고민을 하셨으리라..
고민의 핵심이슈도 비슷할 것이다.

바로 **Flickr vs Picasa, **이것이다.

원래는 블로그 사진 링크를 위해 Flickr를 선택하고 플러그인을 설치했다. Flickr로 결정을 한 것은, 사용중인 스마트폰 노키아 6210이 찍은 사진을 바로 Flickr로 업로드하는 기능이 Default로 있었고, 그걸 이용하면 스마트폰으로 찍은 사진을 블로그에서 바로 보여줄 수 있었기 때문이었다.

그러다가 얼마전 Picasa Desktop을 만났다. 오래 전에 초창기 버전을 다운 받아 써보긴 했지만, 필요가 강하지 않았었는지 그냥 누구나 다 쓰는 알씨로 만족했는데, 위에서 언급한 문제의식을 갖고 다시 써보니, "오~~ 너무 좋은데!, 쓰고 싶다!"
필요를 딱딱 충족해주는 기능. 맘에 든다.

그래서 이런 것들을 고민하게 되었다.


<blockquote>
1. Flickr는 유료 회원 가입하면 저장공간이 무한대인데, Picasa는 공간이 늘어날 때마다 돈을 더 내야 한다. 음...
2. Picasa에 업로드한 사진을 블로그에서 보여주는 플러그인이 필요하다.
3. 스마트폰으로 찍은 사진을 Picasa로 전송하여 블로그로 포스팅하고 싶은데 어떻게 하지?
</blockquote>



다들 했던 고민이고, 해결책들도 있었다.

**1. 비용 이슈**


<blockquote>
- 용량이 늘어날 수록 Flickr가 유리하다. 그런데 속도가 느리다. 웹 UI도 Picasa가 좋다.
- 20G에 5$정도면 돈 낼만하다는 생각이 든다.
- [다른 사람들의 고민과 해결책 구글링](http://www.google.co.kr/search?complete=1&hl=ko&q=flickr+vs+picasa&btnG=Google+%EA%B2%80%EC%83%89&lr=&aq=f)
</blockquote>


**2. Wordpress Plugin for Picasa**


<blockquote>
- [Picasa 사진을 가져와 보여주는 괜찮은 플러그인( Shshin, Michael Toppa)](http://www.toppa.com/shashin-wordpress-plugin/)을 발견했다. 현재 화면 오른쪽에 보이는 것이다.
- 이와 함께 [Lightbox 플러그인](http://stimuli.ca/lightbox/)도 설치했다. thumbnail을 클릭하면 화면 가득 큰 사진이 뜨게 하는 것이다.
- 그림을 삽입 할 때, [Picasa 웹에서 선택하여 삽입할 수 있는 플러그인](http://bogde.ro/computers/picasa-ligthbox-2-preview.htm)도 설치했다. 사진 전송 트래픽을 줄일 수 있다.
- 감당할 수 없이 다양하고 많은 플러그인을 접하면서 Wordpress를 선택하길 잘 했다는 생각이 든다.
</blockquote>


**3. Upload Pics from Phone to Picasa**


<blockquote>
- [이메일을 이용하여 Picasa에 업로드하는 기능](http://picasa.google.com/support/bin/answer.py?answer=83342&hl=ko)을 발견함.
- 전용 이메일 주소를 발급받아 해당 주소로 업로드하면, "Dropbox"라는 앨범에 자동으로 사진이 업로드되는 방식이다.
- 6210에서 사진보기를 할 때, 기본적으로 이메일 전송 옵션이 있으므로 편하게 전송할 수 있다.
</blockquote>



모두 현재 블로그에 적용해서 사용중이다.
