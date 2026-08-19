# Digital Lending Backend

A backend system for managing digital loan applications, eligibility evaluation, loan approvals, repayments, and transaction records through RESTful APIs.

## Overview

The Digital Lending Backend provides APIs for managing the complete loan lifecycle — from user registration and loan application to approval, disbursement, repayment, and loan closure.

The project focuses on applying software engineering principles such as object-oriented design, modular business logic, relational database design, API development, validation, and transaction management.

## Key Features

* User registration and authentication
* Loan application and management
* Rule-based loan eligibility evaluation
* Loan approval and rejection workflow
* EMI calculation
* Automated repayment schedule generation
* Payment processing and transaction history
* Loan status tracking
* Input validation and exception handling
* Prevention of duplicate payments
* RESTful API architecture
* Relational database persistence
* Docker-based deployment

## System Architecture

```text
                    Client
                      |
                      v
                REST API Layer
                      |
                      v
              Business Logic Layer
                      |
          +-----------+-----------+
          |                       |
          v                       v
   Loan/Eligibility          Payment/
      Services               Repayment
          |                       |
          +-----------+-----------+
                      |
                      v
                 MySQL Database
```

## Technology Stack

| Component            | Technology             |
| -------------------- | ---------------------- |
| Programming Language | Python                 |
| Backend Framework    | Flask / FastAPI        |
| API                  | REST                   |
| Database             | MySQL                  |
| ORM                  | SQLAlchemy             |
| Authentication       | JWT                    |
| Containerization     | Docker, Docker Compose |
| Testing              | Pytest                 |
| Version Control      | Git, GitHub            |

## Core Modules

### 1. User Management

Handles user registration, authentication, and profile management.

### 2. Loan Application

Users can submit loan applications containing information such as:

* Loan amount
* Tenure
* Income
* Employment details
* Credit score

### 3. Eligibility Engine

The system evaluates loan applications using predefined eligibility rules.

Example:

```text
Credit Score >= Minimum Score
AND
Income >= Minimum Income
AND
Existing Debt <= Debt Limit
```

Based on these conditions, an application can be marked eligible or rejected.

### 4. Loan Management

Manages the loan lifecycle:

```text
Applied
   ↓
Under Review
   ↓
Approved / Rejected
   ↓
Disbursed
   ↓
Active
   ↓
Closed
```

### 5. EMI & Repayment

The system calculates EMI based on:

* Principal amount
* Interest rate
* Loan tenure

It then generates a repayment schedule and tracks individual installments.

### 6. Payment Management

Records payments and maintains transaction history.

The backend validates payment requests and prevents duplicate processing to maintain consistency.

## Database Design

The system uses a relational MySQL database.

Main entities:

```text
Users
   |
   +---- Loan Applications
                |
                +---- Loans
                       |
                       +---- Repayments
                       |
                       +---- Payments
```

### Main Tables

**Users**

Stores user account and profile information.

**Loan Applications**

Stores applications submitted by users.

**Loans**

Stores approved loan information.

**Repayments**

Stores the repayment schedule for each loan.

**Payments**

Stores completed payment transactions.

Primary and foreign keys are used to maintain relationships between entities.

## Example API Endpoints

### User

```http
POST /api/users/register
POST /api/users/login
GET /api/users/{id}
```

### Loans

```http
POST /api/loans/apply
GET /api/loans/{id}
GET /api/users/{id}/loans
POST /api/loans/{id}/approve
POST /api/loans/{id}/reject
```

### Repayments

```http
GET /api/loans/{id}/repayments
POST /api/repayments/{id}/pay
GET /api/users/{id}/payments
```

## Reliability & Data Consistency

The backend incorporates:

* Input validation
* Exception handling
* Database transactions
* Foreign-key constraints
* Duplicate-payment checks
* Appropriate HTTP status codes
* Structured error responses

These mechanisms help prevent inconsistent loan and payment records.

## Object-Oriented Design

The application separates responsibilities into different components such as:

```text
User
Loan
LoanApplication
Payment
Repayment
EligibilityService
LoanService
PaymentService
```

Business operations are kept separate from API handling and database access to improve maintainability.

## Running the Project

### Clone the repository

```bash
git clone <your-repository-url>
cd digital-lending-backend
```

### Install dependencies

```bash
pip install -r requirements.txt
```

### Configure environment variables

Create a `.env` file:

```env
DATABASE_URL=<your-mysql-database-url>
JWT_SECRET_KEY=<your-secret-key>
```

### Run the application

```bash
python app.py
```

The API will be available locally at:

```text
http://localhost:5000
```

## Docker

The application can be run using Docker Compose:

```bash
docker-compose up --build
```

This starts the backend and database services in isolated containers.

## Testing

Run the test suite using:

```bash
pytest
```

Tests cover API endpoints, business logic, validation, and payment-related scenarios.

## Future Improvements

* Integration with external credit-scoring services
* Integration with UPI/payment gateways
* Asynchronous loan-processing workflows
* Fraud detection
* Rate limiting
* API monitoring and observability
* Caching for frequently accessed loan information
* Event-driven transaction processing

## Learning Outcomes

This project demonstrates practical experience with:

* Object-oriented programming
* Data structures and algorithms
* REST API development
* Relational database design
* SQL and transactions
* Backend architecture
* Error handling and debugging
* Docker-based deployment
* Software engineering and modular design
