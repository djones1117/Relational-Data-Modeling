<img src="https://i.imgur.com/l4t0NOc.png" width="400">

# Relational Data Design & Modeling

## Learning Objectives

| Students will be able to: |
|---|
| Identify the data **entities** for an application |
| Identify **attributes** for a data entity |
| Identify the **relationships** between data entities |
| Understand the roles of **primary** and **foreign keys** |
| Create an **Entity Relationship Diagram (ERD)** for an application |

## Road Map

1. Intro to Data Modeling
2. Data Entities
3. Designing an Entity Relationship Diagram (ERD)
4. Determining the Cardinality Between Entities
5. Summary
6. Essential Questions
7. Further Study

## 1. Intro to Data Modeling

An important part of the planning process for an application is determining the data persistence needs of that application.

This planning results in a **data model**.

The **data model** is conceptual and is used as a blueprint for implementing the data persistence needs within a given database technology (SQL, NoSQL, etc.).

The data model is typically visualized with an **Entity Relationship Diagram** (ERD).

## 2. Data Entities

### What is a Data Entity?

A **Data Entity**, or just **entity**, is used to conceptually model (represent) a real-world object within an application.

Examples:  **User**, **Post**, **Comment**, **Order**, **Product**, etc.

Each entity type will have one or more **attributes**...

### The Attributes for a Data Entity

**Attributes** represent an entity's data. For example, a **Book** entity would probably have a **title** attribute.

Each attribute has a data type. For example, _string_, _numeric_, _datetime_

| Book |
|---|
| title (String) |

### 👉 You Do - Identify Attributes (1 minute)

**Identify what other attributes might a Book entity have?**

<details>
<summary>
Examples
</summary>
<hr>

Examples:

| Book |
|---|
| title (String) |
| isbn (Number) |
| num_pages (Number) |
| is_hardcover (Boolean) |
| forward (String) |
| etc... |

(`author`, `publisher`, etc. would themselves more commonly be entities, not attributes)

<hr>
</details>

### Mapping Between an Entity and a Relational Database

Remember, the conceptual **data model** is used as a **blueprint** for how the actual database will be structured.

Each **entity** in a data model identifies a **table** in a relational database. For example, a **Book** entity will result in a **books** table in the database.

<details>
<summary>
❓In Mongoose (NoSQL), what did entities map to?
</summary>
<hr>

**Schemas**, which may or may not have been compiled into models (embedding just used a schema, not a model)

<hr>
</details>

Each **attribute** in an entity identifies a **column** in the table.  For example, the **title** attribute will result in a column with the same name.

Each **row** in the table would represent an **instance** of the **entity**.

## 3. Designing an Entity Relationship Diagram (ERD)

To learn about data modeling, we'll design an ERD for an application...

### The Sample Application

Let's design an ERD for a Concert Ticket Tracking application.

The application should track:
- The tickets for a concert
- The seat and price of the ticket
- The customer that bought a ticket
- The date of the concert
- The performer(s) of the concert
- The venue of the concert

### The Process

Reviewing an application's **user stories** is a good first step to creating the conceptual data model.

To design a basic ERD, we must identify three different components:
1. The **data entities**
2. The **attributes** (the data properties of an entity)
3. The **relationships** between the entities

Since this application is supposed to track **tickets**, let's start with a preliminary **Ticket** entity...

### The `Ticket` Entity

Here's our first attempt at modeling the **Ticket** entity by including all the attributes you might see printed on a ticket:

<img src="https://i.imgur.com/jcpU8dF.png" height="200">
	
As currently designed above, this is how the data might look like in the **tickets** table:

<img src="https://i.imgur.com/TSDHx6I.png">

However, several of the attributes in our first attempt are actually better defined as **entities** instead.

### Distinguishing Between Attributes and Entities

If you answer "yes" to either of the following questions, the attribute is likely a candidate to be an entity instead:

- Would the attribute likely have attributes of its own? 
- Could the attribute be in common with other entities?  For example, a **Customer** for a Ticket is also likely to be common to other entities like Order, MarketingCampaign, Review, etc.

### 👉 You Do - Identifying Other Data Entities/Attributes (5 mins)

1. Identify which of the attributes we currently have for Ticket:

    <img src="https://i.imgur.com/jcpU8dF.png" height="200">

    ...should actually be **entities** instead.

2. Identify some common attributes for the entities you just identified in step 1.

<details>
<summary>
No Peeking
</summary>
<hr>

**Data Entities Galore!**

<img src="https://i.imgur.com/4iq2IOu.png" width="80%">

<hr>
</details>

### Database Vocabulary - _Database Normalization_

[Database Normalization](https://en.wikipedia.org/wiki/Database_normalization) is the process of designing a relational database to be more efficient by reducing redundancies.

A **relational** database is able to perform searching & updating of data much more efficiently when it is "normalized".

Okay, with the entities and their attributes set for our Concert Ticket Tracking app, let's talk about the third component of the ERD - **relationships** between the entities...

### Relationships Between Entities

Data entities often have a **relationship** with one or more other entities.

**Relationships** determine how the entities are related in terms of their **cardinality**.

There are three main types of cardinality:
- **one-to-one** (1:1)
- **one-to-many** (1:M)
- **many-to-many** (M:M)

#### Example: One-To-One Relationship

A **one-to-one** relationship exists when one row in a table relates to a single row in another table.

Although **1:1** relationships are not as common as **1:M** and **M:M** relationships, they do exist in some data models.

For example:

A **business** has one **mailing address** and vice-versa:

<img src="https://i.imgur.com/VWkbqxi.png">

Let's discuss the connecting lines...

#### ERD Cardinality Lines

In an ERD, lines drawn between entities describe the cardinality between those entities as follows:

<img src="https://i.imgur.com/sEnNZyZ.png">

Note that these are the three main types of cardinality. There are more specific versions of these, such as _zero or many_:

<img src="https://i.imgur.com/JtPQEOO.png">

## 4. Determining the Cardinality Between Entities

Okay, let's model the relationships between the entities of our Concert Ticket Tracking application...

<img src="https://i.imgur.com/4iq2IOu.png">

> 👀 To save screen space, the entities are not going to show attributes for the primary and foreign keys.  However, be aware that as a default, primary keys are named `id` and foreign keys as `<parent_entity_name>_id`.

We can usually determine whether the relationship between two entities is one-to-many or many-to-many by thinking about the relationship in **both directions**.

For example, let's identify the relationship between the `Concert` and `Ticket` entities:

- Can/does a single concert have/belong to more than one ticket? (Answer: **Yes**)
- Can/does a single ticket have/belong to more than one concert? (Answer: **No**)

Therefore the relationship would be<br>
`Concert --< Ticket` (one-to-many)

<img src="https://i.imgur.com/jlKmola.png">

> A Concert has many Tickets" and<br>"A Ticket belongs to a Concert".

<details>
<summary>
❓ Which of the two tables would have to contain the Foreign Key (FK)?
</summary>
<hr>

The **tickets** table - the "belongs to"/child entity will always have the FK.

<hr>
</details>

Let's continue to identify the type of relationship between the following entities...

#### `Customer` and `Ticket`

<details>
<summary>
❓ What's the relationship?
</summary>
<hr>

`Customer --< Ticket` (one-to-many)

<img src="https://i.imgur.com/6Uc4wHF.png">

<hr>
</details>

#### Seems like there should also be a relationship between the **Customer** and **Concert** entities...

Thanks to the way relational databases are designed, you can access other tables that are not directly joined by joining with others that are.

For example, you most certainly could access all of the _concerts_ attended by a _customer_ by joining through _tickets_:

`Customer --< Ticket >-- Concert`

Although not shown on the ERD with a connecting line, you could say that<br>
**"A Customer has many Concerts through Tickets"**, as well as,<br>
**"A Concert has many Customers through Tickets"**.

### 👉 You Do - Identify the Remaining Relationship (2 mins)

Identify the remaining relationships:

- **Concert** and **Venue**
- **Concert** and **Performer**

<details>
<summary>
Don't Peek (final ERD)
</summary>
<hr>

`Venue --< Concert`<br>
`Concert >--< Performer`

<img src="https://i.imgur.com/qz8V0NX.png">

<hr>
</details>

## 5. Summary

Modeling data is an important step during the planning for a project because _**data is the single source of truth**_ of any application!

In addition to what we covered in this lesson, there are several other notations/ways to diagram an application's data model.  Check out [this post](https://www.lucidchart.com/pages/er-diagrams) from _lucidchart.com's_ website for more info.  

## 6. ❓ Essential Questions (1 min)

<details>
<summary>
(1) True or False:  Each Data Entity has its own table in a Relational Database?
</summary>
<hr>

**True**

<hr>
</details>

<details>
<summary>
(2) What would be the relationship between Orders & Products in an eCommerce application?
</summary>
<hr>

**`Order >--< Product`**

<hr>
</details>

<details>
<summary>
(3) In this relationship:<br><code>Customer ---< Order</code><br>which entity (table) would have the Foreign Key?
</summary>
<hr>

The **Order** entity (**orders** table) 

<hr>
</details>

## 7. Further Study

- [What is an Entity Relationship Diagram - Lucidchart](https://www.lucidchart.com/pages/er-diagrams)

- [The Relational Model](https://en.wikipedia.org/wiki/Relational_model)

- [Father of the Relational Model - E. F. Codd](https://en.wikipedia.org/wiki/Edgar_F._Codd)