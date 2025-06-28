# Requirement Analysis in Software Development.

## What is Requirement Analysis?
Requirement Analysis is a critical phase in the software development lifecycle (SDLC) where the project team gathers, analyzes, and defines the requirements of the software product to be developed. This process ensures that all stakeholders have a clear and mutual understanding of what the system should do and how it should perform.

## Why is Requirement Analysis Important?
* **Clarity and Understanding**: It helps in understanding what the stakeholders expect from the software, reducing ambiguity.
* **Scope Definition**: Clearly defines the scope of the project, which helps in preventing scope creep.
* **Basis for Design and Development**: Provides a solid foundation for designing and developing the system.
  
## Key Activities in Requirement Analysis.
### 1. **Requirement Gathering** 🗂️
  * **Interviews**: Conducting interviews with stakeholders to gather detailed information about their needs and expectations.
  * **Surveys/Questionnaires**: Distributing surveys to collect requirements from a larger audience.
* **Workshops**: Organizing workshops with stakeholders to discuss and gather requirements.
* **Observation**: Observing end-users in their working environment to understand their needs.
* **Document Analysis**: Reviewing existing documentation and systems to understand current functionalities and requirements.
### 2. Requirement Elicitation ✍️
* **Brainstorming**: Conducting brainstorming sessions to generate ideas and gather requirements.
* **Focus Groups**: Holding focus group discussions with selected stakeholders to gather detailed requirements.
* **Prototyping**: Creating prototypes to help stakeholders visualize the system and refine their requirements.
### 3. Requirement Documentation 📚
* **Requirement Specification Document**: Creating a detailed document that lists all functional and non-functional requirements.
* **User Stories**: Writing user stories to describe functionalities from the user’s perspective.
* **Use Cases**: Creating use case diagrams to show interactions between users and the system.
### 4. Requirement Analysis and Modeling 📊
* **Requirement Prioritization**: Prioritizing requirements based on their importance and impact on the project.
* **Feasibility Analysis**: Assessing the feasibility of requirements in terms of technical, financial, and time constraints.
* **Modeling**: Creating models (e.g., data flow diagrams, entity-relationship diagrams) to visualize and analyze requirements.
### 5. Requirement Validation ✅
* **Review and Approval**: Reviewing the documented requirements with stakeholders to ensure accuracy and completeness.
* **Acceptance Criteria**: Defining clear acceptance criteria for each requirement to ensure they meet the expected standards.
* **Traceability**: Establishing traceability matrices to ensure all requirements are addressed during development and testing.

## Types of Requirements
### Functional Requirements

These describe **what the system should do** — the specific functions, tasks, or behaviors expected.

### 1. **Hotel Listing Management**
* Hotel managers must be able to:
  * Add, update, or remove hotel listings.
  * Upload room details (photos, price, amenities, availability).

### 2. **Search Functionality**
* Customers should be able to:
  * Search for hotels based on location, price, and other filters.
  * View hotel details from cached results stored in **Elasticsearch**.

### 3. **Booking Functionality**
* Customers must be able to:
  * Select rooms and dates.
  * Initiate a hotel room booking via a Booking Service.
  * Confirm booking with payment through a **third-party payment provider**.

### 4. **Payment Integration**
* The system must:
  * Process secure payments.
  * Confirm transactions and update booking status.
  * Notify users and hotel managers upon successful booking.

### 5. **Booking History View**
* Customers and hotel managers can:
  * View past and upcoming bookings.
  * Access recent bookings from Redis (cache) and older bookings from Cassandra.

### 6. **Notification System**
* Notifications must be sent to:
  * Hotel managers when a booking is made.
  * Customers when a booking is confirmed or an offer is available.

### 7. **Data Synchronization**
* Any change in hotel or booking data should:
  * Be sent to **Kafka**.
  * Be updated across services (Elasticsearch for search, Cassandra for archive, CDN for delivery).


### **Non-Functional Requirements**
These define **how the system should perform** rather than what it should do.

### 1. **Performance & Response Time**
* Search results and booking responses must be fast (target: < 2 seconds).
* Redis caching and Elasticsearch indexing ensure reduced latency.

### 2. **Scalability**
* The system should handle thousands of concurrent users.
* Use of **microservices**, **load balancers**, and **replicated databases** (master-slave) helps scale horizontally.

### 3. **Reliability**
* Ensures no double bookings or missing records.
* Booking confirmation should be atomic and fail-safe.

### 4. **Availability**
* System must provide **99.9% uptime**, using distributed services and backups.

### 5. **Fault Tolerance**
* If one microservice fails (e.g., payment), others continue to work independently.
* Messaging queues like Kafka help retry or buffer failed operations.

### 6. **Data Consistency**
* Write operations use master DB, while read operations go to slave DB.
* Messaging queue ensures eventual consistency across services (e.g., booking DB, Cassandra, CDN).

### 7. **Security**
* Encrypt all sensitive customer data and payment transactions.
* Ensure API access is authorized and logged.

### 8. **Maintainability**
* Code is modular through services (Hotel Service, Booking Service, Notification Service, etc.).
* Easy to update or redeploy individual services without affecting the whole system.

### 9. **Extensibility**
* Easily integrate new features like loyalty rewards or coupon systems using APIs and event-driven architecture.

## Use Case Diagrams
What are Use Case Diagrams?
Use case diagrams show how different users (actors) interact with the system to achieve specific goals (use cases).

### Creating Use Case Diagrams:
* Identify actors (e.g., guest, registered user, admin).
* Define use cases (e.g., search properties, book property, manage listings).
* Draw interactions between actors and use cases.

### Benefits of Use Case Diagrams:
* Provide a clear visual representation of system functionalities.

* Help in identifying and organizing system requirements.
* Facilitate communication among stakeholders and development team.

![alx-booking-uc.png](https://github.com/user-attachments/assets/dbf965e5-9642-4341-9d9b-a5ead4f77bb9)

## Acceptance Criteria.
Acceptance criteria are conditions that a feature must meet to be accepted by the stakeholders.

### Benefits of Acceptance Criteria:
* Ensure all parties have a clear understanding of feature requirements.
* Provide a basis for testing and validation.
* Help in maintaining quality and meeting user expectations.

### Example of Acceptance criteria
**Given** a customer has selected their booking details and is ready to checkout
**When** they proceed to the checkout page
**Then** they should see a complete booking summary including:
* Service/room details with dates and duration
* Itemized price breakdown (base price, taxes, fees)
* Selected add-ons or upgrades
* Total amount due
* Cancellation and refund policy
