---
​---
layout: post
​---
---

# ubuntu 심볼릭 링크 만들기

윈도우의 '바로가기'같은 것이 심볼릭 링크로서, 우분투에서 복잡한 디렉토리 구조를 단순화해서 쉽게 찾아갈 수 있도록 해주는 것이다. 아래와 같은 명령어로 간단하게 만들 수 있다.

```shell
ln -sf [원래 폴더 패스] [심볼릭 링크]
```

예를 들면, 아래와 같이 할 수 있다.

```shell
ln -sf /home/me/complex/folder/place /myfolder
cd /
cd myfolder
```

이렇게 해서 만들어진 폴더 색깔은 하늘색이다.





