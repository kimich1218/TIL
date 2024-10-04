# JOIN 쿼리
단일 엔티티에 대한 정보를 공유하는 테이블은 데이터베이스 전체에서 해당 엔티티를 고유하게 식별하는 기본 키를 가져야 한다. 

쿼리에서 JOIN 절을 사용하여 이 고유 키를 기준으로 두 개의 별도 테이블의 행 데이터를 결합할 수 있다.

#### INNER JOIN을 사용하는 SELECT 쿼리
INNER JOIN은 첫 번째 테이블과 두 번째 테이블의 동일한 키를 가진 행을 일치시켜 두 테이블의 결합된 열을 가지 결과 행을 생성하는 과정이다.
```sql
SELECT 열, 다른_테이블_열, …
FROM mytable
INNER JOIN another_table 
    ON mytable.id = another_table.id
WHERE 조건
ORDER BY 열, … ASC/DESC
LIMIT 행_수 OFFSET 시작_위치;
```

INNER JOIN은 두 테이블 모두에 존재하는 데이터만을 포함하는 결과 테이블을 생성한다. 하지만 데이터가 비대칭적인 경우, 즉 서로 다른 단계에서 데이터가 입력되어 두 테이블에 일치하는 데이터가 없는 경우,  **LEFT JOIN**, **RIGHT JOIN**, 또는 **FULL JOIN**을 사용 할 수 있다.

#### LEFT/RIGHT/FULL JOIN을 사용하는 SELECT 쿼리
세 가지 JOIN도 INNER와 마찬가지로 어떤 열을 기준으로 데이터를 결합할 것인지 지정해야 한다. 테이블 A를 테이블 B와 조인할 때, **LEFT JOIN**은 B에서 일치하는 행이 없어도 A의 행을 포함한다. **RIGHT JOIN**은 그 반대이다. B의 행을 유지하되, A에서 일치하는 행이 없어도 B의 행을 포함한다. 마지막으로, **FULL JOIN**은 두 테이블 모두의 행을 유지하며, 상대 테이블에 일치하는 행이 없는 경우에도 포함한다.
```sql
SELECT 열, 다른_열, …
FROM mytable
INNER/LEFT/RIGHT/FULL JOIN another_table 
    ON mytable.id = another_table.matching_id
WHERE 조건
ORDER BY 열, … ASC/DESC
LIMIT 행_수 OFFSET 시작_위치;
```