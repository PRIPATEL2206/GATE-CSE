# SQL & Relational Algebra

> Subject: Databases
> GATE weight: **3–6 marks** every year. Relational algebra ops, SQL queries, joins, aggregates, NULL handling.

---

## 1. Concept Explanation

### 1.1 Relational Algebra

Procedural language for queries. **Operations:**

| Operator | Symbol | Description |
|---|---|---|
| **Selection** | σ | Choose rows |
| **Projection** | π | Choose columns |
| **Union** | ∪ | Combine rows (set) |
| **Set Difference** | − | Rows in A not in B |
| **Cartesian Product** | × | All pairs |
| **Rename** | ρ | Rename relation/attributes |
| **Intersection** | ∩ | Common rows |
| **Join (θ-join)** | ⋈ | Conditional combine |
| **Natural Join** | ⋈ | Join on common attributes |
| **Equi-join** | ⋈ | Join with equality |
| **Outer Joins** | ⟕, ⟖, ⟗ | Left, right, full outer |
| **Division** | ÷ | "All matching" semantics |

### 1.2 Selection σ

`σ_condition(R)` returns tuples of R satisfying condition.

Example: `σ_(age > 30)(Employee)`.

### 1.3 Projection π

`π_attributes(R)` returns relation with only those attributes.

Removes duplicates (since relation is set).

Example: `π_(name, salary)(Employee)`.

### 1.4 Union, Intersection, Difference

Both relations must have **same arity and compatible domains** (union compatible).

`R ∪ S`: rows in either.
`R ∩ S`: rows in both.
`R − S`: rows in R but not S.

### 1.5 Cartesian Product

`R × S` produces all combinations.

For |R|·|S| total rows.

### 1.6 Joins

**θ-join:** `R ⋈_θ S = σ_θ(R × S)`. Condition θ is any predicate.

**Equi-join:** θ uses only equality.

**Natural join:** equi-join on attributes with same name; one copy retained.

**Outer joins** preserve unmatched rows from one or both sides.

### 1.7 Division

`R ÷ S` returns tuples in R that match all of S.

Example: students who took **all** courses in S.

Useful for "for all" queries.

### 1.8 Rename ρ

`ρ_NewName(R)` renames relation; `ρ_S(A→B)(R)` renames attribute A to B.

### 1.9 SQL Overview

**SQL = Structured Query Language.** Standard for relational DBs.

| Sublanguage | Description |
|---|---|
| **DDL** | Schema (CREATE, ALTER, DROP) |
| **DML** | Data (SELECT, INSERT, UPDATE, DELETE) |
| **DCL** | Permissions (GRANT, REVOKE) |
| **TCL** | Transaction (COMMIT, ROLLBACK, SAVEPOINT) |

### 1.10 SELECT Syntax

```sql
SELECT [DISTINCT] columns
FROM tables
WHERE condition
GROUP BY columns
HAVING condition
ORDER BY columns [ASC | DESC]
LIMIT n;
```

### 1.11 SELECT Operations

| Operation | Example |
|---|---|
| Project | `SELECT name FROM Emp` |
| Filter | `WHERE salary > 50000` |
| Sort | `ORDER BY salary DESC` |
| Distinct | `SELECT DISTINCT dept` |
| Limit | `LIMIT 10` |

### 1.12 Aggregate Functions

| Function | Description |
|---|---|
| `COUNT(*)` | Number of rows |
| `COUNT(col)` | Non-NULL count |
| `SUM(col)` | Sum |
| `AVG(col)` | Average |
| `MIN(col)`, `MAX(col)` | Extremes |

### 1.13 GROUP BY and HAVING

`GROUP BY` aggregates rows per group.
`HAVING` filters groups (post-aggregation).

```sql
SELECT dept, AVG(salary)
FROM Emp
GROUP BY dept
HAVING AVG(salary) > 50000;
```

### 1.14 Joins in SQL

| Type | Syntax | Description |
|---|---|---|
| **INNER JOIN** | `R JOIN S ON cond` | Matched rows only |
| **LEFT JOIN** | `R LEFT JOIN S ON cond` | All from R + matches |
| **RIGHT JOIN** | `R RIGHT JOIN S ON cond` | All from S + matches |
| **FULL JOIN** | `R FULL JOIN S ON cond` | All rows |
| **CROSS JOIN** | `R CROSS JOIN S` | Cartesian |
| **NATURAL JOIN** | `R NATURAL JOIN S` | On common attributes |
| **SELF JOIN** | `R r1 JOIN R r2` | Join table to itself |

### 1.15 Set Operations

```sql
SELECT ... UNION SELECT ...
SELECT ... INTERSECT SELECT ...
SELECT ... EXCEPT SELECT ...    -- (or MINUS)
```

`UNION ALL` keeps duplicates; `UNION` removes them.

### 1.16 Subqueries

| Type | Description |
|---|---|
| **Scalar** | Returns single value |
| **Row** | Returns single row |
| **Table** | Returns table |
| **Correlated** | Refers to outer query |

```sql
SELECT * FROM Emp
WHERE salary > (SELECT AVG(salary) FROM Emp);
```

**EXISTS / NOT EXISTS:**
```sql
SELECT * FROM Emp e
WHERE EXISTS (SELECT 1 FROM Dept d WHERE d.id = e.dept_id);
```

**IN / NOT IN:**
```sql
SELECT * FROM Emp WHERE dept_id IN (1, 2, 3);
```

### 1.17 NULL Handling

NULL = unknown value.

| Comparison | Result |
|---|---|
| NULL = NULL | NULL (not TRUE) |
| NULL <> anything | NULL |
| NOT NULL | NULL |
| `IS NULL` / `IS NOT NULL` | TRUE / FALSE |

**3-valued logic:** TRUE / FALSE / UNKNOWN.

`COUNT(*)` counts all rows; `COUNT(col)` skips NULL.

### 1.18 INSERT, UPDATE, DELETE

```sql
INSERT INTO Emp VALUES (1, 'Alice', 50000);
INSERT INTO Emp(name, salary) VALUES ('Bob', 60000);

UPDATE Emp SET salary = salary * 1.1 WHERE dept = 'IT';

DELETE FROM Emp WHERE id = 5;
```

### 1.19 DDL

```sql
CREATE TABLE Emp (
  id INT PRIMARY KEY,
  name VARCHAR(50) NOT NULL,
  salary DECIMAL(10,2) DEFAULT 0,
  dept_id INT,
  FOREIGN KEY (dept_id) REFERENCES Dept(id) ON DELETE CASCADE
);

ALTER TABLE Emp ADD COLUMN age INT;
ALTER TABLE Emp DROP COLUMN age;

DROP TABLE Emp;
```

### 1.20 Views

```sql
CREATE VIEW HighSalary AS
SELECT name, salary FROM Emp WHERE salary > 50000;
```

Views are virtual tables. Can be **materialized** (cached).

### 1.21 Indexes

Speed up queries by maintaining sorted/hashed structure on columns.

```sql
CREATE INDEX idx_dept ON Emp(dept_id);
```

### 1.22 Stored Procedures & Triggers

**Stored procedure:** named DB function.
**Trigger:** runs in response to event (INSERT/UPDATE/DELETE).

### 1.23 Normalization (preview)

(See [normalization.md](normalization.md).)

### 1.24 Common Query Patterns

**Top N per group:**
```sql
SELECT * FROM (
  SELECT *, ROW_NUMBER() OVER (PARTITION BY dept ORDER BY salary DESC) rn
  FROM Emp
) WHERE rn <= 3;
```

**Self-join (find pairs):**
```sql
SELECT a.name, b.name
FROM Emp a JOIN Emp b ON a.dept = b.dept AND a.id < b.id;
```

**Anti-join:**
```sql
SELECT * FROM Emp WHERE id NOT IN (SELECT mgr_id FROM Dept);
```

> **Summary:** Relational algebra has 6 fundamental ops + derived. SQL is its declarative form. Joins (inner/left/right/full/cross/natural/self), aggregates with GROUP BY/HAVING, subqueries, NULL with 3-valued logic.

---

## 2. Important Points

- **Relational algebra is procedural;** SQL is **declarative**.
- **Selection** (σ) filters rows; **projection** (π) selects columns.
- **Natural join** uses common attribute names.
- **Cartesian product** creates all pairs.
- **Outer joins** preserve unmatched rows.
- **Division** for "for all" queries.
- **NULL** is unknown; uses 3-valued logic.
- **`COUNT(*) ≠ COUNT(col)`** when NULLs present.
- **GROUP BY before SELECT;** HAVING filters groups.
- **Subqueries:** correlated vs non-correlated.
- **EXISTS / NOT EXISTS** for membership tests.
- **UNION removes duplicates;** UNION ALL keeps them.
- **DISTINCT** removes duplicate rows.
- **JOIN ON vs USING vs NATURAL** subtle differences.
- **WHERE filters before grouping;** HAVING after.

---

## 3. Short Notes

```
RELATIONAL ALGEBRA
 σ selection
 π projection
 ∪ ∩ − set ops (union compatible)
 × Cartesian product
 ρ rename
 ⋈ θ-join, equi-join, natural
 ⟕ ⟖ ⟗ outer joins
 ÷ division ("for all")

SQL CATEGORIES
 DDL: CREATE, ALTER, DROP
 DML: SELECT, INSERT, UPDATE, DELETE
 DCL: GRANT, REVOKE
 TCL: COMMIT, ROLLBACK, SAVEPOINT

SELECT
 SELECT [DISTINCT] cols
 FROM tables
 WHERE row-cond
 GROUP BY cols
 HAVING group-cond
 ORDER BY cols [ASC|DESC]
 LIMIT n

AGGREGATES
 COUNT(*)/COUNT(col), SUM, AVG, MIN, MAX

GROUP BY: aggregate per group
HAVING: filter groups (post-aggregation)

JOINS
 INNER, LEFT, RIGHT, FULL, CROSS, NATURAL, SELF

SET OPS
 UNION (de-dup), UNION ALL (keep dup)
 INTERSECT, EXCEPT/MINUS

SUBQUERIES
 scalar, row, table
 correlated vs non-correlated
 EXISTS / NOT EXISTS
 IN / NOT IN

NULL
 3-valued logic (T/F/UNKNOWN)
 IS NULL / IS NOT NULL
 NULL = NULL is NULL

INSERT / UPDATE / DELETE

DDL
 CREATE TABLE; PK; FK + ON DELETE
 ALTER ADD/DROP/MODIFY
 DROP TABLE

VIEWS: CREATE VIEW
INDEXES: CREATE INDEX

PROCEDURES, TRIGGERS
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | σ filter rows; π select cols | ✅✅ |
| 2 | Natural join: common attribute equality | ✅✅ |
| 3 | UNION removes duplicates; UNION ALL keeps | ✅✅ |
| 4 | NULL = NULL is NULL (use IS NULL) | ✅✅ |
| 5 | COUNT(*) vs COUNT(col): NULL handling | ✅✅ |
| 6 | GROUP BY before HAVING | ✅✅ |
| 7 | SQL clause order: WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT | ✅ |
| 8 | LEFT JOIN preserves left side | ✅ |
| 9 | EXISTS for membership | ✅ |
| 10 | Division for "for all" queries | ✅ |
| 11 | DDL/DML/DCL/TCL classes | ✅ |
| 12 | Views virtual; can be materialized | ✅ |

### Tricks

- **Convert SQL to relational algebra:** SELECT → π, WHERE → σ, FROM → ×/⋈.
- **For "all of X":** use division or NOT EXISTS.
- **For top-N per group:** window function or subquery.
- **For NULLs:** use IS NULL / IS NOT NULL, not = NULL.
- **For aggregate with grouping:** GROUP BY required for non-aggregate columns.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
σ_C(R) returns:
**Solution.** Tuples of R satisfying C.

### Q2. (GATE CSE 2014)
Natural join requires:
**Solution.** Common attribute names with equality.

### Q3. (GATE CSE 2018)
NULL = NULL evaluates to:
**Solution.** NULL (not TRUE).

### Q4. (GATE CSE 2008)
COUNT(*) vs COUNT(col):
**Solution.** Skips NULLs in COUNT(col).

### Q5. (GATE CSE 2010)
SQL clause order:
**Solution.** WHERE → GROUP BY → HAVING → SELECT → ORDER BY.

### Q6. (GATE CSE 2015)
Outer join preserves:
**Solution.** Unmatched rows from one or both sides.

### Q7. (GATE CSE 2013)
Division operation example:
**Solution.** Students enrolled in **all** courses in S.

### Q8. (GATE CSE 2007)
GROUP BY without aggregation:
**Solution.** Returns distinct rows.

### Q9. (GATE CSE 2003)
UNION vs UNION ALL:
**Solution.** UNION removes duplicates.

### Q10. (GATE CSE 2009)
Self-join:
**Solution.** Join table to itself with aliases.

### Q11. (GATE CSE 2019)
Correlated subquery:
**Solution.** Refers to outer query.

### Q12. (GATE CSE 2020)
View vs materialized view:
**Solution.** Virtual vs cached.

### Q13. (GATE CSE 2021)
Trigger:
**Solution.** Runs on event.

### Q14. (GATE CSE 2016)
HAVING vs WHERE:
**Solution.** HAVING after grouping; WHERE before.

### Q15. (GATE CSE 2011)
Cross join produces:
**Solution.** Cartesian product.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Selection symbol?

**P2.** Projection symbol?

**P3.** Natural join uses what?

**P4.** UNION removes duplicates?

**P5.** NULL behavior in equality.

**P6.** Aggregate functions list.

**P7.** GROUP BY purpose.

**P8.** HAVING vs WHERE.

**P9.** SQL clause execution order.

**P10.** EXISTS purpose.

### Medium

**P11.** Write σ for "salary > 50000".

**P12.** Convert `SELECT name FROM Emp WHERE age > 30` to relational algebra.

**P13.** Inner join two tables on common column.

**P14.** Compute aggregate per department.

**P15.** Find max salary per department.

**P16.** Find employees in departments with > 5 people.

**P17.** Use EXISTS to find departments with employees.

**P18.** Convert M:N relationship to SQL.

**P19.** Apply UPDATE with WHERE.

**P20.** DELETE based on subquery.

### Hard

**P21.** Implement division using basic algebra ops.

**P22.** Self-join: find pairs in same dept.

**P23.** Correlated subquery for top-N per group.

**P24.** Anti-join for missing FK.

**P25.** Window function for ranking.

**P26.** Recursive CTE for hierarchy.

**P27.** Trigger to enforce business rule.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | σ | direct |
| P2 | π | direct |
| P3 | common attribute equality | direct |
| P4 | yes | direct |
| P5 | NULL | direct |
| P6 | COUNT, SUM, AVG, MIN, MAX | direct |
| P7 | aggregate per group | direct |
| P8 | post vs pre group | direct |
| P9 | WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT | direct |
| P10 | membership test | direct |
| P11 | σ_(salary > 50000)(Emp) | direct |
| P12 | π_name(σ_(age > 30)(Emp)) | direct |
| P13 | INNER JOIN | direct |
| P14 | GROUP BY dept | direct |
| P15 | MAX with GROUP BY | direct |
| P16 | HAVING COUNT(*) > 5 | direct |
| P17 | EXISTS subquery | direct |
| P18 | join via association table | direct |
| P19 | direct | direct |
| P20 | direct | direct |
| P21 | π and − operations | direct |
| P22 | aliases | direct |
| P23 | ROW_NUMBER over partition | direct |
| P24 | NOT IN / NOT EXISTS | direct |
| P25 | RANK / DENSE_RANK / ROW_NUMBER | direct |
| P26 | WITH RECURSIVE | direct |
| P27 | BEFORE INSERT trigger | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | NULL = NULL is TRUE | It's NULL. |
| 2 | COUNT(*) skips NULL | It counts all rows. |
| 3 | HAVING before GROUP BY | After. |
| 4 | NATURAL JOIN ambiguity | Common names matter. |
| 5 | GROUP BY missing non-aggregated columns | Required in standard SQL. |
| 6 | NOT IN with NULL | Returns no rows; use NOT EXISTS. |
| 7 | UNION keeps duplicates | UNION ALL does. |
| 8 | DISTINCT slow | Sometimes; depends on indexes. |
| 9 | Outer join order matters | LEFT vs RIGHT. |
| 10 | Aggregate without GROUP BY | Returns single row. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Select rows" | σ / WHERE. |
| "Select columns" | π / SELECT. |
| "All matching" | Division / NOT EXISTS. |
| "Group by attribute" | GROUP BY. |
| "Filter groups" | HAVING. |
| "Top N per group" | Window function. |
| "Find missing" | Anti-join. |
| "NULL handling" | IS NULL / IS NOT NULL. |
| "Outer join" | LEFT/RIGHT/FULL. |
| "Aggregate query" | COUNT/SUM/AVG/MIN/MAX. |

---

## 9. Quick Revision

```
RELATIONAL ALGEBRA
 σ selection, π projection
 ∪, ∩, − (union compatible)
 × Cartesian
 ρ rename
 ⋈ join (θ, equi, natural)
 ⟕ ⟖ ⟗ outer
 ÷ division (for all)

SQL CATEGORIES
 DDL, DML, DCL, TCL

SELECT clause order
 FROM → WHERE → GROUP BY → HAVING
 → SELECT → ORDER BY → LIMIT

AGGREGATES: COUNT, SUM, AVG, MIN, MAX
GROUP BY + HAVING

JOINS
 INNER / LEFT / RIGHT / FULL
 CROSS / NATURAL / SELF

SET OPS
 UNION (dedup) / UNION ALL / INTERSECT / EXCEPT

SUBQUERIES
 scalar / row / table
 correlated vs non-correlated
 EXISTS / NOT EXISTS / IN / NOT IN

NULL
 3-valued logic
 IS NULL / IS NOT NULL
 NULL = NULL is NULL
 COUNT(*) vs COUNT(col)

DDL: CREATE, ALTER, DROP
TCL: COMMIT, ROLLBACK, SAVEPOINT

VIEW (virtual) / MATERIALIZED VIEW (cached)
INDEX for performance
TRIGGER on event
```
