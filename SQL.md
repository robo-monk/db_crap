# SQL
How to program SQL queries good!!!!11!! FREE COURSE LINK IN DESCRIPTION

In comments are the relational algebra representation of the queries


## Intro
```sql
select * from hero, has_alias
-- hero × has_alias

select * from hero h, has_alias ha
	where h.id = ha.hero_id

-- lame: σ[id=hero_id] hero x has_alias
-- good: hero ⨝ [id=hero_id] has_alias
```

## JOINS
### Inner JOIN
* List students & their exam results
```sql
select lastname, course, result from student as s
	join exam as e on s.std_id=e.std_id
-- π[lastname, course, result] (Student ⨝ [student.std_id=exam.std_id] exam)
```
### Left Outer JOIN
* List all students & their exam results if any
```sql
select lastname, course, result from student as s 
	left join exam as e on s.std_id = e.std_id
-- π[lastname, course, result] (Student ⟕ [student.std_id=exam.std_id] exam)
```

### Right Outer JOIN
* List all exam results & their respective student
``` sql
select lastname, course, result from student as s
	right join exam as e on s.std_id = e.std_id

-- π[lastname, course, result] (Student ⟖ [student.std_id=exam.std_id] exam)
```

### Full Outer JOIN
* List all students & all exams respetive to each other (if relation exists)
``` sql
select lastname, course, result from student as s
	full join exam as e on s.std_id = e.std_id

-- π[lastname, course, result] (Student ⟗ [student.std_id=exam.std_id] exam)
```

## Sets

```sql
((select course, result from exam
	where course = 100)
	except
		(select course, result from exam
			where result is null))
	union values ( 100, 7.5), (100, 9)

```

## Subqueries

```sql
select hero.* from hero, has_power p
where hero.id = p.hero
	and power_strength = (
		select max(power_strength)
		from has_power
	)
-- select all heroes having power with max strength

select * from hero where id in (
	select hero from has_alias
	where alias_name like 'Super%'
)

-- slect all those heroes having an alias starting with super

select * from hero h
where exists (
	select * from has_alias a where h.id = a.hero
)
-- select heroes having at least one alias
-- semijoin


select h.real_name, a.alias_name
from has_alias a, (
	select * from hero where real_name like 'A%'
)
where h.id < 100 and a.hero = h.id
-- get real name, alias for all heroes with a real name starting with a and an id smaller than 100


with hero_num_powers as (
	select hero as h_id, count(*) as num_pow
	-- (temp. table)
)
select * from hero h
	join hero_num_powers hnp on h.id = hnp.h_id
where hnp.num_pow = (
	select max(num_pow) from hero_num_powers
)

-- select heroes having most powers
```


