# SQL

SQL은 [SQL 고득점 Kit](https://school.programmers.co.kr/learn/challenges?tab=sql_practice_kit)를 메인으로 공부함

- 기본적은 문법은 다음과 같음

    ```sql
    SELECT 
    FROM
    (JOIN    ON)
    (WHERE)
    (GROUP BY)
    (HAVING)
    ```
- ```JOIN```


### 문제
- [그룹별 조건에 맞는 식당 목록 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/131124)
    ```
    WITH T AS (
        SELECT MEMBER_ID, COUNT (MEMBER_ID) as cnt
        FROM REST_REVIEW
        GROUP BY MEMBER_ID
    ),

    M AS (
        SELECT t.MEMBER_ID, p.MEMBER_NAME
        FROM T t JOIN MEMBER_PROFILE p
        ON t.MEMBER_ID = p.MEMBER_ID
        WHERE cnt = (SELECT MAX(cnt) FROM T)
    )

    SELECT m.MEMBER_NAME, r.REVIEW_TEXT, DATE_FORMAT(r.REVIEW_DATE, "%Y-%m-%d") AS REVIEW_DATE
    FROM M m JOIN REST_REVIEW r
    ON m.MEMBER_ID = r.MEMBER_ID
    ORDER BY 3, 2
    ```
### 피드백


