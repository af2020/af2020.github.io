---
layout: post
---
# shell script
shell script를 어떻게 사용하는지에 대해서 간단히 방법을 적어보겠습니다.
아래와 같은 목차로 할 예정입니다.

## 작성
아래와 같이 .sh 파일을 작성할 때, 파일의 첫줄에 이 파일이 스크립트 파일인 것을 적시함 

```sehll
#! /bin/bash
```

ubuntu 명령어를 순차적으로 입력하면 순차적으로 실행됨. 예를 들어, 작성된 블로그 .md 파일의 git push를 위해 아래와 같이 스크립트 파일을 만들어 실행할 수 있음

```shell
#! /bin/bash
git status
git add .
git status
git commit -m 'commit by script'
git push
echo "mission accomplished!"

```

그리고, 해당 파일에 실행권한을 주어서 실행가능하도록 함

```shell
chmod +x test.sh
```



## 실행
실행은 아래와 같이 함

```shell
./test.sh
```

