# ER Model & Relational Model

> Subject: Databases
> GATE weight: **2–4 marks** every year. ER design, mapping cardinality, ER → relational, integrity constraints.

---

## 1. Concept Explanation

### 1.1 ER (Entity-Relationship) Model

A **conceptual** data model representing the structure of data using:
- **Entities** — real-world objects.
- **Relationships** — associations between entities.
- **Attributes** — properties.

### 1.2 Entity & Entity Set

- **Entity:** a "thing" (e.g., an employee).
- **Entity set:** collection of similar entities.

Represented by **rectangle**.

### 1.3 Attributes

| Type | Description |
|---|---|
| **Simple** | Atomic (e.g., age) |
| **Composite** | Decomposable (e.g., name → first + last) |
| **Derived** | Computed (e.g., age from DOB) |
| **Multi-valued** | Multiple values (e.g., phone numbers) |
| **Key** | Uniquely identifies entity |

ER notation:
- Ellipse: attribute.
- Double ellipse: multi-valued.
- Dashed ellipse: derived.
- Underlined: key attribute.

### 1.4 Relationships

Connect entities. Represented by **diamond**.

**Degree:** number of entities involved.
- **Unary** (recursive): relates same entity to itself.
- **Binary:** 2 entities.
- **Ternary, n-ary:** 3+ entities.

### 1.5 Mapping Cardinality

For binary relationship between A and B:

| Type | Description |
|---|---|
| **One-to-One (1:1)** | Each A maps to ≤ 1 B and vice versa |
| **One-to-Many (1:N)** | Each A maps to ≥ 0 B; each B maps to ≤ 1 A |
| **Many-to-One (N:1)** | Reverse |
| **Many-to-Many (M:N)** | Each A may relate to many B and vice versa |

### 1.6 Participation Constraint

| Type | Description |
|---|---|
| **Total** | Every entity must participate (double line) |
| **Partial** | Some may not (single line) |

### 1.7 Keys

| Key | Description |
|---|---|
| **Super key** | Set of attributes uniquely identifying entity |
| **Candidate key** | Minimal super key |
| **Primary key** | Chosen candidate key |
| **Alternate key** | Other candidate keys |
| **Foreign key** | Refers to primary key in another relation |
| **Composite key** | Multiple attributes |
| **Surrogate key** | Synthetic (e.g., auto-increment) |

### 1.8 Weak Entity Set

Entity that lacks sufficient attributes to form a primary key.
- Identified via **identifying relationship** with **owner entity**.
- Has **partial key** (discriminator).
- Drawn with **double rectangle**.

### 1.9 Specialization & Generalization (IS-A)

| Term | Description |
|---|---|
| **Specialization** | Top-down: split entity into sub-entities |
| **Generalization** | Bottom-up: combine entities into super-entity |
| **Disjoint** | Sub-entities don't overlap |
| **Overlapping** | Sub-entities can share members |
| **Total** | Every super-entity must be in some sub |
| **Partial** | Not required |

### 1.10 Aggregation

Treat a relationship as a higher-level entity.
Used to model relationships among relationships.

### 1.11 ER Diagram → Relational Schema

**Strong entity set:**
- Create relation with all attributes.
- Primary key = ER key.

**Weak entity set:**
- Create relation with weak's attributes + owner's key.
- PK = (owner key + discriminator).

**1:1 relationship:**
- Add foreign key to either side (typically the partial side).

**1:N relationship:**
- FK on **N side** referencing 1 side.

**M:N relationship:**
- Create new relation with both PKs.

**Multi-valued attribute:**
- Create separate relation (entity key + value).

**Composite attribute:**
- Flatten into atomic attributes.

### 1.12 Relational Model

Data organized into **relations (tables)**:
- **Relation = set of tuples** (no duplicates).
- **Schema:** structure (column names + types).
- **Instance:** current state.
- **Tuple = row;** **Attribute = column.**

### 1.13 Domain & Atomicity

Each attribute has a **domain** (allowed values).
Each value must be **atomic** (1NF).

### 1.14 Integrity Constraints

| Constraint | Description |
|---|---|
| **Domain** | Value must be in attribute's domain |
| **Entity integrity** | Primary key not null |
| **Referential integrity** | FK references existing PK (or NULL) |
| **Key constraint** | Unique values in PK / unique keys |
| **Check** | User-defined predicate |

### 1.15 Referential Integrity Actions

When referenced row deleted/updated:
- **CASCADE:** propagate change.
- **SET NULL:** make FK null.
- **SET DEFAULT:** to default value.
- **RESTRICT / NO ACTION:** prevent.

### 1.16 Schema vs Instance

- **Schema:** like type (structure).
- **Instance:** like value (current data).

Schema rarely changes; instance frequently.

### 1.17 Reduction Examples

**Strong entity Employee(EmpID, Name, Salary):**
```
Employee(EmpID, Name, Salary)
PK = EmpID
```

**Weak entity Dependent(Name, Birthday) of Employee:**
```
Dependent(EmpID, Name, Birthday)
PK = (EmpID, Name);  EmpID FK → Employee
```

**1:N relationship Works_For (Employee → Dept):**
```
Employee(EmpID, ..., DeptID)   — DeptID FK
```

**M:N relationship Enrolls (Student × Course):**
```
Enrolls(StudentID, CourseID, Grade)
PK = (StudentID, CourseID)
StudentID FK; CourseID FK
```

### 1.18 Specialization Mapping

3 approaches:
1. **One relation per type** (super + each sub with FK).
2. **One relation per sub** (no super) — only for total.
3. **One single relation** (all attributes + type indicator) — flat.

### 1.19 Constraints in ER

| Constraint | Description |
|---|---|
| Cardinality | 1:1, 1:N, M:N |
| Participation | Total / partial |
| Keys | Identifying attributes |
| Domain | Attribute value range |

### 1.20 Common GATE Patterns

- ER diagram → relational schema mapping.
- Identify number of relations needed.
- Determine PK and FK after mapping.
- Cardinality interpretation.

> **Summary:** ER model = entities + relationships + attributes. Cardinality (1:1, 1:N, M:N), participation (total/partial). Reduce ER to relations: M:N gets its own table; 1:N FK on N-side; weak entities use owner's key. Integrity constraints enforce data validity.

---

## 2. Important Points

- **Weak entity** has no own PK; uses owner's + discriminator.
- **M:N** always becomes a separate relation.
- **1:N FK** is on the N side.
- **Multi-valued attribute** becomes a separate relation.
- **Foreign key** can be NULL (if not part of PK).
- **Entity integrity:** PK never NULL.
- **Referential integrity:** FK references valid PK or is NULL.
- **Generalization vs specialization** are inverse processes.
- **Aggregation** treats relationship as entity.
- **Composite key:** multiple attributes form PK together.
- **Surrogate keys** are synthetic (e.g., serial IDs).
- **CASCADE / SET NULL / RESTRICT** govern FK update/delete.
- **Each relation must have a PK.**
- **Atomicity (1NF)** required in basic relational model.

---

## 3. Short Notes

```
ER MODEL
 entity / relationship / attribute
 entity set: rectangle
 relationship: diamond
 attribute: ellipse

ATTRIBUTES
 simple, composite, derived,
 multi-valued (double ellipse), key (underline)

DEGREE: unary / binary / ternary / n-ary

CARDINALITY: 1:1 / 1:N / N:1 / M:N

PARTICIPATION: total (double line) / partial

KEYS
 super key, candidate, primary, alternate,
 foreign, composite, surrogate

WEAK ENTITY
 no PK; identifying relationship + owner
 PK = owner's PK + discriminator
 double rectangle

SPECIALIZATION (top-down)
GENERALIZATION (bottom-up)
 disjoint / overlapping
 total / partial
 IS-A relationship

AGGREGATION: relationship as entity

ER → RELATIONAL
 strong entity → table
 weak entity → table with owner's PK
 1:1 → FK on either side
 1:N → FK on N side
 M:N → new table with both PKs
 multi-valued → separate relation

RELATIONAL
 relation = set of tuples
 schema (structure) vs instance (data)
 atomic values (1NF)

INTEGRITY
 domain
 entity (PK not null)
 referential (FK valid)
 key, check

FK ACTIONS
 CASCADE / SET NULL / SET DEFAULT / RESTRICT

SPECIALIZATION MAPPING
 type 1: super + subs
 type 2: only subs (total only)
 type 3: single flat relation
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | M:N → separate relation | ✅✅ |
| 2 | 1:N → FK on N side | ✅✅ |
| 3 | Weak entity → owner's PK + discriminator | ✅✅ |
| 4 | Multi-valued attribute → separate relation | ✅ |
| 5 | Entity integrity: PK ≠ NULL | ✅✅ |
| 6 | Referential integrity: FK valid or NULL | ✅✅ |
| 7 | Cardinality types: 1:1, 1:N, N:1, M:N | ✅✅ |
| 8 | Participation: total / partial | ✅ |
| 9 | Specialization mapping (3 ways) | ✅ |
| 10 | Aggregation = relationship as entity | ✅ |

### Tricks

- **Quick relation count:** strong entities + M:N relationships + multi-valued attributes.
- **For cardinality:** 1:1 can merge tables; 1:N puts FK on N side.
- **Weak entity always needs owner's key.**
- **For composite attribute:** flatten to atomic attributes.
- **For total participation:** sometimes can merge into stronger constraint.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
M:N relationship in relational schema:
**Solution.** Separate relation with both PKs as composite PK.

### Q2. (GATE CSE 2014)
Foreign key can be:
**Solution.** NULL or reference existing PK.

### Q3. (GATE CSE 2018)
Weak entity has:
**Solution.** No own PK; uses owner's + discriminator.

### Q4. (GATE CSE 2008)
Cardinality 1:N FK location:
**Solution.** On N side.

### Q5. (GATE CSE 2010)
Number of tables for ER with 3 strong entities + 2 M:N relationships:
**Solution.** 3 + 2 = 5 tables.

### Q6. (GATE CSE 2015)
Total participation indicator:
**Solution.** Double line.

### Q7. (GATE CSE 2013)
Generalization vs specialization:
**Solution.** Bottom-up vs top-down.

### Q8. (GATE CSE 2007)
Composite key definition:
**Solution.** Multiple attributes form PK.

### Q9. (GATE CSE 2003)
Atomic attribute:
**Solution.** Indivisible value.

### Q10. (GATE CSE 2009)
Entity integrity:
**Solution.** PK is not NULL.

### Q11. (GATE CSE 2019)
Multi-valued attribute mapping:
**Solution.** Separate relation.

### Q12. (GATE CSE 2020)
Aggregation in ER:
**Solution.** Treat relationship as entity.

### Q13. (GATE CSE 2021)
1:1 relationship FK:
**Solution.** Either side.

### Q14. (GATE CSE 2016)
Surrogate key example:
**Solution.** Auto-increment ID.

### Q15. (GATE CSE 2011)
Referential action CASCADE:
**Solution.** Propagate update/delete.

---

## 6. Practice Questions (20+)

### Easy

**P1.** Define entity.

**P2.** Define relationship.

**P3.** Cardinality types.

**P4.** Total vs partial participation.

**P5.** Super key vs candidate key.

**P6.** PK vs FK.

**P7.** Composite key.

**P8.** Weak entity.

**P9.** Multi-valued attribute mapping.

**P10.** Referential integrity.

### Medium

**P11.** Map M:N relationship to relational schema.

**P12.** Map 1:N relationship.

**P13.** Map weak entity.

**P14.** Composite + multi-valued attribute mapping.

**P15.** Specialization mapping (3 strategies).

**P16.** Identify cardinality from constraints.

**P17.** Determine # tables for given ER.

**P18.** ER diagram for university (students, courses, enrollment).

**P19.** Identify keys from set of attributes.

**P20.** Apply CASCADE on delete.

### Hard

**P21.** Reduce complete ER diagram to relations.

**P22.** Draw ER for hospital management.

**P23.** Compare 3 specialization mapping strategies.

**P24.** Resolve referential integrity violation.

**P25.** Identify weak entity in given scenario.

**P26.** Aggregate relationship in ER for project assignments.

**P27.** Design schema for online retail.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | thing in real world | direct |
| P2 | association between entities | direct |
| P3 | 1:1, 1:N, N:1, M:N | direct |
| P4 | every vs some | direct |
| P5 | superset vs minimal | direct |
| P6 | identifies vs references | direct |
| P7 | multiple attribute PK | direct |
| P8 | no own PK | direct |
| P9 | separate relation | direct |
| P10 | FK valid | direct |
| P11 | new relation with both keys | direct |
| P12 | FK on N side | direct |
| P13 | owner's key + discriminator | direct |
| P14 | flatten + separate relation | direct |
| P15 | super+subs / subs only / flat | direct |
| P16 | check constraints | direct |
| P17 | strong + M:N + multi-valued | direct |
| P18 | 3 entities + enrollment table | direct |
| P19 | uniqueness + minimality | direct |
| P20 | propagate | direct |
| P21 | step-by-step | direct |
| P22 | patient/doctor/visit | direct |
| P23 | trade-offs | direct |
| P24 | enforce or fix data | direct |
| P25 | dependent on owner | direct |
| P26 | aggregation | direct |
| P27 | customer/product/order | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | M:N as FK only | Need separate relation. |
| 2 | Weak entity has own PK | Uses owner's key. |
| 3 | FK on 1 side in 1:N | Should be N side. |
| 4 | Forget atomicity (1NF) | Required. |
| 5 | NULL in PK | Violates entity integrity. |
| 6 | Mixing PK and unique | Both can have unique constraint; PK is special. |
| 7 | Cardinality direction confusion | Read both sides. |
| 8 | Treating composite as multi-valued | Different. |
| 9 | Specialization vs generalization swapped | Top-down vs bottom-up. |
| 10 | Aggregation = generalization | Different. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "ER → relational" | Apply mapping rules. |
| "Number of tables" | Strong + M:N + multi-valued. |
| "Cardinality" | 1:1, 1:N, M:N. |
| "Weak entity" | Owner's PK + discriminator. |
| "FK action CASCADE" | Propagate. |
| "Total participation" | Double line. |
| "Generalization" | Bottom-up. |
| "Multi-valued mapping" | Separate relation. |
| "Composite mapping" | Flatten. |
| "Aggregation" | Relationship as entity. |

---

## 9. Quick Revision

```
ER MODEL: entity / relationship / attribute

ATTRIBUTES: simple / composite / derived / multi-valued / key

CARDINALITY: 1:1 / 1:N / N:1 / M:N
PARTICIPATION: total / partial

KEYS
 super, candidate, primary, alternate,
 foreign, composite, surrogate

WEAK ENTITY: no PK; uses owner's

GENERALIZATION (up) / SPECIALIZATION (down)
 disjoint / overlapping
 total / partial

AGGREGATION: relationship as entity

ER → RELATIONAL
 strong → table
 weak → table with owner's PK
 1:N → FK on N
 M:N → new table with both PKs
 multi-valued → separate relation

INTEGRITY
 domain, entity (PK not null), referential (FK valid)

FK ACTIONS
 CASCADE / SET NULL / SET DEFAULT / RESTRICT

ATOMICITY (1NF)
```
