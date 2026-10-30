# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:

<img width="1532" height="870" alt="dbms exp 1 a" src="https://github.com/user-attachments/assets/c64c4960-c2ce-4ac2-8627-a4b2fa4ace50" />

<img width="1263" height="660" alt="Screenshot 2026-10-27 143039" src="https://github.com/user-attachments/assets/966f1e66-7f85-4fa9-8eed-7a8d22ad8b30" />


### Entities and Attributes

### Entities

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Member | **member_id (PK)**, first_name, last_name, gender, phone_no | Strong entity. `member_id` is not in the diagram, so it is added as a PK. |
| Program | **program_id (PK)**, name, duration | Strong entity. |
| Trainer | **trainer_id (PK)**, name, phone_no | Strong entity. |
| Training Session | **session_id (PK)**, time, trainer_id (FK), member_id (FK) | Strong entity. The FKs come from the `mentor` and `book` relationships. |
| Payment | **payment_id (PK)**, date, amount | Strong entity. `payment_id` is not in the diagram, so it is added as a PK. |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Enroll (Member – Program) | M:N | Member: partial, Program: partial | Relationship attributes: `date`, `status`. Becomes a junction table `Enroll(member_id, program_id, date, status)`. |
| Conduct (Program – Trainer) | N:1 (a trainer conducts many programs) | Program: total, Trainer: partial | `trainer_id` goes in Program as an FK. |
| Book (Member – Training Session) | 1:N (a member books many sessions) | Member: partial, Session: total | `member_id` goes in Training Session as an FK. |
| Mentor (Trainer – Training Session) | 1:N (a trainer mentors many sessions) | Trainer: partial, Session: total | `trainer_id` goes in Training Session as an FK. |
| Makes (Member – Payment) | M:N (as labelled in the diagram) | Member: total, Payment: total (double lines) | Needs a junction table `Makes(member_id, payment_id)`. |

### Assumptions
- 
- 
- 

---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
<img width="1528" height="924" alt="dbms exp 1 b" src="https://github.com/user-attachments/assets/83e6fefe-2535-43e1-b8dd-5eae27de3ddf" />

<img width="1267" height="667" alt="Screenshot 2026-10-30 203000" src="https://github.com/user-attachments/assets/e707ea60-38f9-44b7-b6f7-9119a937a9d2" />



### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Member | MemberID (PK), FirstName, LastName, Gender, PhoneNo | Member details |
| Book | BookID (PK), Title, Category, Duration | Book details |
| Speaker | SpeakerID (PK), Name, PhoneNo | Speaker details |
| Event | EventID (PK), Time, MemberID (FK), RoomID (FK) | Event details |
| Room | RoomID (PK), Room, Location | Room details |
| Loan | LoanID (PK), Date, MemberID (FK) | Loan details |
| Fine | FineID (PK), Amount, Reason, LoanID (FK) | Fine details |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Member – Book | M:N | Partial – Partial | Member borrows books |
| Book – Speaker | M:N | Partial – Partial | Book features speakers |
| Member – Loan | 1:N | Partial – Total | Member has multiple loans |
| Member – Event | M:N | Partial – Partial | Member registers for events |
| Event – Room | N:1 | Total – Partial | Event books a room |
| Loan – Fine | 1:0..1 | Partial – Total | Loan generates a fine |


### Assumptions
- 
- 
- 

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:

<img width="1225" height="692" alt="Screenshot 2026-10-30 204045" src="https://github.com/user-attachments/assets/a13bbf32-f0f6-4933-8a6a-7fab3775fc73" />

<img width="1556" height="983" alt="dbms exp 1 c" src="https://github.com/user-attachments/assets/6c2d47fb-385d-4759-8938-dce2b4e62f2d" />



### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Customer | Email (PK), FirstName, LastName, PhoneNo | Customer details |
| Reservation | ReservationID (PK), Date, Time, NumberOfGuests, CustomerEmail (FK), TableID (FK) | Reservation details |
| Table | TableID (PK), Name, PhoneNo, WaiterID (FK) | Table details |
| Waiter | WaiterID (PK), PhoneNo | Waiter details |
| Order | OrderID (PK), Time, CustomerEmail (FK), WaiterID (FK) | Order details |
| Bill | BillID (PK), Tax, TotalAmount, OrderID (FK) | Billing details |
| Dish | DishID (PK), Name, Description, Amount, CategoryID (FK) | Dish details |
| Category | CategoryID (PK), Name | Category details |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Customer – Reservation | 1:N | Partial – Total | Customer creates reservations |
| Reservation – Table | N:1 | Total – Partial | Reservation uses a table |
| Table – Waiter | N:1 | Total – Partial | Table managed by waiter |
| Waiter – Order | 1:N | Partial – Total | Waiter handles orders |
| Customer – Order | 1:N | Partial – Total | Customer places orders |
| Order – Dish | M:N | Partial – Partial | Order contains dishes |
| Category – Dish | 1:N | Partial – Total | Dish belongs to category |
| Order – Bill | 1:1 | Total – Total | Order has a bill |

### Assumptions
- 
- 
- 

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
