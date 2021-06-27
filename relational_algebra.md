# Relational Algebra

## Operations

#### Set operations
* Union ∪
* Intersection ∩
* Diff ∖
* Cartesian Product ×

##### Cartesian Product
A = [ 1, 2, 3 ]
B = [ a, b, c ]

A × B = [ (1,a),(1,b),(1,c),(2,a),(2,b),(2,c),(3,a),(3,b),(3,c) ]


#### Relational operations
* Selection σ
* Projecting π
* Renaming ρ

## σ 
##### σ[sex=female] (students)
* select all female students
* `select * from students where sex=female`

##### σ[course=100 && result>=3.0] (exams)
* `select * from exams where course=100 && result>=3.0`


## π
* retains only collumns with given names
* if tuples are identical after projection, duplicate tuples are removed

##### π[title] (Courses)
* `select title from courses`

##### π[firstName, lastName] σ[sex=female] (students)
* `select firstName, lastName from students where sex=female`


## Algebra Set Operators

##### σ[crs_no=100] (Course) ∪ σ[crs_no=102] (Course)
```sql
select * from course where crs_no=100
union
select * from course where crs_no=102
```

## ρ
* unary operation 
* give names explicitly to the fields of a relation instance
* break large RA into smaller subexpressions
* similar to SQL's As



