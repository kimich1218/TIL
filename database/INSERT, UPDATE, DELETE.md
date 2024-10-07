# INSERT, UPDATE, DELETE
### INSERT
새 데이터를 삽입하기 위해서는 INSERT를 사용해야 한다. 데이터를 삽입할 테이블, 열, 행을 지정한다. 보통 각 행은 테이블의 모든 열에 대한 값을 포함해야 하지만, 경우에 따라 열만 명시하고 기본값을 사용할 수 있다.

**모든 열에 대한 값을 지정하는 INSERT 문**
```sql
INSERT INTO mytable
VALUES (value_or_expr, another_value_or_expr, …),
       (value_or_expr_2, another_value_or_expr_2, …),
       …;
```

### UPDATE
기존 데이터를 업데이트를 하기 위해서는 UPDATE 문을 사용해야 한다.

**값으로 행을 업데이터하는 UPDATE 문**
```sql
UPDATE mytable
SET column = value_or_expr, 
    other_column = another_value_or_expr, 
    …
WHERE condition;
```

### DELETE
데이터베이스 테이블을 삭제하려면 DELETE 문을 삭제해야 한다.

**조건이 포함된 DELETE 문**
WHERE 조건을 생략하면 모든 행이 제거된다.
```sql
DELETE FROM mytable
WHERE condition;
```
