---
author: admin
comments: false
date: 2012-06-01 11:51:17+00:00
layout: post
link: http://hubnode.cafe24.com/wp/archives/1667
slug: matlab-oracle-database-connection
title: matlab oracle database connection
wordpress_id: 1667
---

Matlab Database toolbox를 이용하여 oracle database를 가져오는 것을 정리함.

1. oracle ODBC 설정


<blockquote>(제어판 >> 관리도구 >> 데이터 원본(ODBC))</blockquote>


2. Database 연결


<blockquote>_conn_ = database ('DBName', 'ID', 'Password')</blockquote>


3. Data 객체 (Cursor) 생성


<blockquote>_curs_ = exec(_conn_, 'select * from testdb')</blockquote>


4. fetch


<blockquote>_curs_ = fetch(_curs_, 100)</blockquote>


5. Matlab 변수 생성


<blockquote>_matlab_data_ = _curs_.data</blockquote>


Matlab 최고!
