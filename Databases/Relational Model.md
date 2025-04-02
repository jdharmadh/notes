- A **database** is a collection of relations. 
- A **relation** $R \subseteq S_1 \times S_2 \times ... \times S_n$ is a subset of the possible tuples, where each $S_i$ is the domain of attribute $i$ 
- A tuple is an element of $S_1 \times S_2 \times ... \times S_n$ 
- Rows in a relation:
	- Ordering does not matter (a relation is a set)
	- Rows could be distinct (this is called **set semantics**)
	- Rows could be duplicated (this is called **bag semantics**)
- Columns in a relation:
	- Ordering is important (but ideally it shouldn't be)
	- Domain of each column is a primitive type
### Schema
- A **relation schema** describes column heads
	- Relation name
	- Name of each field (aka attribute)
	- Domain of each field
- The **degree** or **arity** of a relation is the number of attributes
- A **database schema** is the set of all relation schemas

### Instance
- An **instance** of a relation is a concrete instantiation of that instance (e.g. a table). it must be a set of tuples matching the schema. 
- The **cardinality** of a relation instance is the number of tuples it has
- An instance of a database is a set of relation instances

### Integrity Constraints
- Condition specified on a database schema, restricts data that can be stored in the database
- DBMS should enforce integrity constraints
- Simple: domain constraint, each attribute's value must match domain specified in schema
- Key Constraints:
	- Super Key: Set of attributes that determines all other attributes
	- Key: Minimal super key
	- Primary key: One minimal key can be selected as primary key
	- Foreign key: field refers to the primary key of other relation
### Relational Algebra
- Queries specified in an operational manner (step-by-step procedure)
- **Relational operators** take one or two relation instances as an argument and return a relational instance as a result. They are easy to compose into relational algebra expressions.
	- Selection: Condition is boolean combination of atomic predicates
	- Projection: Filter some columns and discard the rest
	- Union
	- Set Difference
	- Cartesian product / Join

#### Joins
- Theta-join: join with a condition, cross product followed by selection
- Equijoin: join with a condition that consists only of equalities, projection drops redundant attributes
- Natural join: equijoin, but equality on all fields with same name