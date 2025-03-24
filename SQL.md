# SQL

SQL은 [SQL 고득점 Kit](https://school.programmers.co.kr/learn/challenges?tab=sql_practice_kit)를 메인으로 공부함

### 피드백
- 가장 기본인데, 문제 잘 읽기 <br>
    출력해야할 column이나 출력 순서 확인안해서 자꾸 틀림

---

### Point
- 기본적인 문법은 다음과 같음

    ```sql
    SELECT 
    FROM
    (JOIN    ON)
    (WHERE)
    (GROUP BY)
    (HAVING)
    ```
- ```BETWEEN A AND B```은 **A 이상 B 이하**
- 조건문 사용법
    ```sql
    SELECT IF(10 > 5, "참", "거짓");

    SELECT 
        CASE 
            WHEN age > 5 THEN "참"
            ELSE "거짓"
        END AS age
    ```
- 윈도우 함수
    - ROW_NUMBER :: 각 행에 index 번호 
        ```sql
        ROW_NUMBER() OVER (PARTITION BY group_column ORDER BY sort_column) AS row_num
        -- PARTITION BY : 그룹 별로 초기화
        -- ORDER BY : 순번 부여 순서
        ```

---
### 문제
<details>
<summary> <a herf = "https://school.programmers.co.kr/learn/courses/30/lessons/131124"> 그룹별 조건에 맞는 식당 목록 출력하기 </a> </summary>
<div>

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

</div>
</details>