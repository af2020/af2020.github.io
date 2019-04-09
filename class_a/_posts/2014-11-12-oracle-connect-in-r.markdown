---
author: admin
comments: false
date: 2014-11-12 10:23:11+00:00
layout: post
link: http://hubnode.cafe24.com/wp/archives/2040
slug: oracle-connect-in-r
title: oracle connect in R
wordpress_id: 2040
---

할 때마다 구글링해가며 찾아봐야 하는 설정인데, 이 참에 정리해보자

1. Oracle Products Download



<blockquote>
[http://www.oracle.com/technetwork/topics/winsoft-085727.html](http://www.oracle.com/technetwork/topics/winsoft-085727.html)

아래와 같이 제공하고 있다. 

> * Instant Client Package - Basic
> 

> * Instant Client Package - SQL*Plus
> 

> * Instant Client Package - ODBC
> 

> * Instant Client Package - JDBC
> 

> * Instant Client Package - SDK
> 


</blockquote>



2. Oracle Products Install



<blockquote>

> * 다운 받은 제품들을 하나의 폴더[ex)d:oracle]에 모두 압축해제
> 
</blockquote>





3. system variable setting


<blockquote>
아래와 같이 환경 변수 설정

1. TNS_ADMIN = d:oracle
2. path = d:oracle;%PATH%
3. LD_LIBRARY_PATH=d:oracle
</blockquote>




4. create tnsnames.ora 



<blockquote>
위의 압축해제 폴더(ex)d:oracle) 안에 tnsnames.ora 파일을 생성하여 접속정보를 입력한다. 파일 내용은 아래와 같다. 뚱뚱한 글씨로 쓴 부분이 접속 정보에 맞도록 변경할 부분.

**DBNAME** =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = **localhost**)(PORT = **1521**))
    )
    (CONNECT_DATA =
      (SERVICE_NAME = **DEV**)
    )
  )
</blockquote>




5. sqlplus test




<blockquote>
이제 sql*plus를 실행하여 접속 테스트를 해보자.
cmd 창을 열고 아래와 같이 입력.
> sqlplus id/password@localhost:1521/DEV


</blockquote>






6. windows odbc setting



<blockquote>
1. 제어판 >> 관리도구 >> 데이터 원본(ODBC)
2. 사용자DSN 탭에서 "추가" 버튼 클릭
3. 드라이버 종류애서 "Oracle in instant10_2" 선택하고 "마침" 버튼
4. DB 접속정보 입력
5. 사용자 데이터 원본 목록에서 추가한 드라이버가 있는지 확인

</blockquote>



7. RODBC Package installing




<blockquote>
[http://cran.r-project.org/web/packages/RODBC/index.html](http://cran.r-project.org/web/packages/RODBC/index.html)
다운 받아 R Library 폴더에 넣음
온라인 상황이라면,
install.packages("RODBC")
그리고,
library(RODBC)
</blockquote>



8. connection generation 




<blockquote>

con <- odbcConnect("DEV", uid="userid", pwd="password")
</blockquote>



9. query test





<blockquote>
test <- sqlQuery(con, "select * From tset_table")

</blockquote>




* 참조




<blockquote>

> * [http://www.wolfpack.pe.kr/210](http://www.wolfpack.pe.kr/210)
> 

> * [http://rprogramming.net/connect-to-database-in-r/](http://rprogramming.net/connect-to-database-in-r/)
> 
</blockquote>



