---
layout: single
title:  "[SQL] 3-1 그룹(aggregate) 함수"
categories: [Database]
tags: [Database, SQL]

toc: true
toc_sticky: true
toc_label: "목차"
---
데이터 집합에 대해서 동작하는 그룹(aggregate) 함수는 대표적으로 네 가지가 있다.


1. COUNT()

2. MIN()과 MAX()

3. SUM()

4. AVG()

---

## GROUP BY 절

GROUP BY 절은 선택된 레코드의 집합을 필드의 값이나 표현식에 의해 그룹화한 결과 집합을 반환한다.

즉, GROUP BY 절은 하나의 그룹을 하나의 레코드로 반환하므로, 결과 집합의 크기를 줄여주는 역할을 한다.



이러한 GROUP BY 절은 SELECT 문에서만 사용할 수 있으며, 앞서 살펴 본 그룹 함수를 사용할 때 자주 같이 사용한다.

```sql
SELECT 필드이름, 그룹함수(필드이름)
FROM 테이블이름
[WHERE 조건]
GROUP BY 필드이름;
```

- rental 테이블에서 user_id가 같은 데이터가 몇 개 있는지 검색

  ```sql
  SELECT user_id, COUNT(*)
  FROM rental
  GROUP BY user_id;
  ```

## HAVING 절

HAVING 절은 SELECT 문의 WHERE 절처럼 **GROUP BY 절에 의해 반환되는 결과 집합의 조건을 설정**할 수 있게 해준다.

```sql
SELECT 필드이름, 그룹함수(필드이름)
FROM 테이블이름
[WHERE 조건]
GROUP BY 필드이름
HAVING 조건;
```

- rental 테이블에서 user_id가 같은 1개 초과의 데이터가 몇 개 있는지 검색

  ```sql
  SELECT user_id, COUNT(*) AS ID_CNT
  FROM rental
  GROUP BY user_id
  HAVING ID_CNT > 1;
  ```

  

  
