# SQL Commands

## User-Defined Variables
- User-defined variables can be declared with `@*var_name*`.
- They are session-specific and are not case sensitive.
- Way to declare user-defined variables is through `SET`.
```
SET @var_name = expr [, @var_name = expr] ...
```
- Assignment operators: `=` or `:=`.

### = and := Operators
- In `SET`, both are assignment operators. 
- In other context, = is a comparison operator.

## Pivot Tables in SQL 
- The following is based on [this problem](https://www.hackerrank.com/challenges/occupations/problem).

**Step 1: Create CASE to print out all data according to occupation**
```
SELECT
    case when Occupation='Doctor' then Name end as Doctor,
    case when Occupation='Professor' then Name end as Professor,
    case when Occupation='Singer' then Name end as Singer,
    case when Occupation='Actor' then Name end as Actor
FROM OCCUPATIONS
```

**Step 2: Create CASE to print out row numbers corresponding to non-NULL values**
```
set @r1=0, @r2=0, @r3=0, @r4=0;

SELECT case 
	when Occupation='Doctor' then (@r1:=@r1+1)
        when Occupation='Professor' then (@r2:=@r2+1)
        when Occupation='Singer' then (@r3:=@r3+1)
        when Occupation='Actor' then (@r4:=@r4+1) end as RowNumber

FROM OCCUPATIONS
```

**Step 3: Combine results from Step 1 and Step 2**
```
set @r1=0, @r2=0, @r3=0, @r4=0;

SELECT case 
	when Occupation='Doctor' then (@r1:=@r1+1)
        when Occupation='Professor' then (@r2:=@r2+1)
        when Occupation='Singer' then (@r3:=@r3+1)
        when Occupation='Actor' then (@r4:=@r4+1) end as RowNumber,
        case when Occupation='Doctor' then Name end as Doctor,
        case when Occupation='Professor' then Name end as Professor,
        case when Occupation='Singer' then Name end as Singer,
        case when Occupation='Actor' then Name end as Actor

FROM OCCUPATIONS
```

**Step 4: Determine the first non-NULL value in each column with MIN/MAX**
```
set @r1=0, @r2=0, @r3=0, @r4=0;
select min(Doctor), min(Professor), min(Singer), min(Actor)
from(
  select case when Occupation='Doctor' then (@r1:=@r1+1)
            when Occupation='Professor' then (@r2:=@r2+1)
            when Occupation='Singer' then (@r3:=@r3+1)
            when Occupation='Actor' then (@r4:=@r4+1) end as RowNumber,
    case when Occupation='Doctor' then Name end as Doctor,
    case when Occupation='Professor' then Name end as Professor,
    case when Occupation='Singer' then Name end as Singer,
    case when Occupation='Actor' then Name end as Actor
  from OCCUPATIONS
  order by Name
	) temp
group by RowNumber;
```
Grouping by RowNumber allows us to print multiple rows, grouped by the row number for each occupation.
