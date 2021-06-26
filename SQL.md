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

