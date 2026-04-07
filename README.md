#  Fitness Influencer Coaching Platform - ER Diagram

##  Overview

This project represents the database design for a **Fitness Influencer Coaching Platform**, where trainers provide online coaching services including plans, consultations, subscriptions, and progress tracking.

The system is designed to handle:

* Trainer and client management
* Coaching plans and subscriptions
* Session scheduling (consultations)
* Progress tracking (check-ins & logs)
* Payment management

---

##  Business Understanding

This is not a traditional gym system. It is an **online coaching ecosystem** where:

* Trainers can manage multiple clients
* Clients can subscribe to multiple plans over time
* Plans can be subscribed to by many clients
* Sessions and check-ins are separate concepts
* Progress tracking is handled independently

---

##  Entities and Description

###  User

Stores basic information for both trainers and clients.

Attributes:

* user_id (PK)
* name
* email
* phone
* role (trainer/client)
* created_at

---

###  Trainer_Profile

Stores trainer-specific details.

Attributes:

* trainer_id (PK, FK → User)
* bio
* experience
* specialization

---

###  Client_Profile

Stores client-specific details.

Attributes:

* client_id (PK, FK → User)
* age
* gender
* height
* goal

---

###  Plan

Represents coaching programs created by trainers.

Attributes:

* plan_id (PK)
* trainer_id (FK)
* name
* description
* duration_days
* price

---

###  Subscription

Represents a client purchasing a plan.

Attributes:

* subscription_id (PK)
* client_id (FK)
* plan_id (FK)
* start_date
* end_date
* status

---

###  Session

Represents consultations or meetings.

Attributes:

* session_id (PK)
* trainer_id (FK)
* client_id (FK)
* subscription_id (FK)
* scheduled_at
* status
* notes

---

###  Check_In

Represents structured weekly progress reports.

Attributes:

* checkin_id (PK)
* client_id (FK)
* trainer_id (FK)
* subscription_id (FK)
* date
* weight
* body_fat
* notes

---

###  Progress_Log

Stores flexible metric-based progress tracking.

Attributes:

* progress_id (PK)
* client_id (FK)
* subscription_id (FK)
* metric_type
* value
* recorded_at

---

###  Payment

Stores payment details for subscriptions.

Attributes:

* payment_id (PK)
* subscription_id (FK)
* amount
* payment_date
* status
* method

---

##  Relationships & Cardinality

* One User → One Trainer_Profile (1:1)

* One User → One Client_Profile (1:1)

* One Trainer → Many Plans (1:N)

* One Client → Many Subscriptions (1:N)

* One Plan → Many Subscriptions (1:N)

* One Subscription → Many Sessions (1:N)

* One Subscription → Many Check-Ins (1:N)

* One Subscription → Many Progress Logs (1:N)

* One Trainer → Many Sessions (1:N)

* One Client → Many Sessions (1:N)

* One Client → Many Check-Ins (1:N)

* One Trainer → Many Check-Ins (1:N)

* One Client → Many Progress Logs (1:N)

* One Subscription → Many Payments (1:N)

---

##  Key Design Decisions

###  Subscription as Core Entity

Acts as a bridge between clients and plans, enabling:

* Multiple clients per plan
* Multiple plans per client over time

---

###  Separation of Session and Check-In

* Sessions = meetings/consultations
* Check-ins = structured progress updates

---

###  Progress Tracking Design

* Check-ins → structured weekly reports
* Progress logs → flexible metric tracking

---

###  Payment Linked to Subscription

Allows:

* Installments
* Retry payments
* Real-world flexibility

---

##  Assumptions

* A user can either be a trainer or a client
* A client can subscribe to multiple plans over time
* Trainers can handle multiple clients simultaneously
* Progress is tracked over time using logs and check-ins

---

##  Notes

* The system is normalized and avoids redundancy
* Junction-like behavior is handled through Subscription
* Designed for scalability and real-world usage

---


##  Conclusion

This ER design provides a scalable and practical foundation for an online fitness coaching platform, covering all essential aspects such as subscriptions, sessions, and progress tracking.
