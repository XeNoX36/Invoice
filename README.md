## Schema
```sql
-- Years wise loan amount
select *
from Finance_1
```
```sql
select *
from Finance_2
```

## 1. Years wise loan amount
```sql
select year(issue_d) as Year_of_issue_d, sum(loan_amnt) as Total_amnt
from Finance_1
group by year(issue_d)
order by Year_of_issue_d
```
## 2. Grade and sub grade wise revol_bal
```sql
select f1.grade, f1.sub_grade, sum(F2.revol_bal) as total_revol_bal
from Finance_1 as F1 join Finance_2 as F2
on f1.id = f2.id
group by f1.grade, f1.sub_grade
order by f1.grade, f1.sub_grade
```
## 3. Total payment for verified and non verified status
```sql 
select f1.verification_status, round(sum(f2.total_pymnt), 2) as total_payment
from Finance_1 as F1 join Finance_2 as F2
on f1.id = f2.id
group by f1.verification_status
order by f1.verification_status 
-- to covert to millions
select f1.verification_status, 
concat(format(round(sum(f2.total_pymnt)/1000000, 2), 'c'), 'M') as total_payment
from Finance_1 as F1 join Finance_2 as F2
on f1.id = f2.id
group by f1.verification_status
order by f1.verification_status 
```
## 4
```sql
select f1.addr_state, f2.last_credit_pull_d, f1.loan_status
from Finance_1 as F1 join Finance_2 as F2
on f1.id = f2.id
group by f1.addr_state, f2.last_credit_pull_d, f1.loan_status
order by f2.last_credit_pull_d 
```

## 5
```sql
select f1.home_ownership, f2.last_pymnt_d
from Finance_1 as F1 join Finance_2 as F2
on f1.id = f2.id
group by f1.home_ownership, f2.last_pymnt_d
order by f1.home_ownership desc, f2.last_pymnt_d desc
```
