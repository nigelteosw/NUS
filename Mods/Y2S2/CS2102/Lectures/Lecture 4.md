# ER Model

## Entity Relationship
### Core Concepts
-   All data is described in terms of
    -   **entities** (rectangle, nouns)
    -   **relationships** (diamond, verbs)
-   **Attributes** describes information about entities and relationships
-   Elements are connected via lines
-   Certain data constraints can be described using _additional annotations_

#### Entity
An **entity** is a _representation_ of real-world objects that are _distinguishable_ from other objects (e.g., user, airport, flight, or booking).

#### Attribute
**Attributes** are specific information _describing an entity_
-   Represented by an **oval** in ER diagrams
##### Subtypes:
1.  **Key Attributes:** **underlined**
    -   Uniquely identifies each entity (uid)
2.  **Composite Attributes:** **composed of other ovals**
    -   Composed of multiple other attributes (address)
3.  **Multivalued Attributes:** **double-lined**
    -   One or more values for a given entity (phone)
4.  **Derived Attributes:** **dashed line**
    -   Derived from other attributes (age)


## Cardinality Constraint
### Many-to-Many
### Many-to-One
### One-to-One


## Participation Constraint
### Total Participation
- Each user booking includes **at least 1** flight and each flight can be part of **0 or more** bookings.
### Key + Total Participation
- Each user can make **0 or more** bookings and each booking can be made by **exactly 1** user.

![[Pasted image 20230221215351.png]]