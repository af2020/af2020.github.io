---
author: admin
comments: true
date: 2011-12-21 14:58:11+00:00
layout: post
link: http://hubnode.cafe24.com/wp/archives/1602
slug: oracle-index-%ec%a1%b0%ed%9a%8c
title: Oracle Index 조회, 생성, 삭제
wordpress_id: 1602
---

# oracle index 조회, 생성, 삭제



## 조회

```sql
select * from user_ind_columns;
select * from user_indexes;
```



## 생성

```sql
create index [index name] on [테이블이름](컬럼이름);
```



## 삭제

```sql
drop index [index name];
```







