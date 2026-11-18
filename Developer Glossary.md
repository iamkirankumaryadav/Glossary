# Basic Architecture 🏗️

### Frontend, backend, and services are the core layers of modern software architecture. 
- Frontend: The visual user interface (UI) we interact with (see, click, type, scroll, etc.)
- Backend: The behind-the-scenes, handling business logic, calculations, and database operations.
- Services: Modular, specialized backend components either built internally or provided by third parties, that perform specific tasks.

### How They Compare
Feature |	Frontend |	Backend |	Services
:--- | :--- | :--- | :---
Also Known As	| Client-side, UI (User Interface). |	Server-side, Core Application. |	Microservices, APIs, Third-Party Integrations.
Primary Role | Display information and capture user actions. | Process data, enforce security, and manage databases. |	Execute one focused task (e.g., payments, emails, AI).
Where It Runs |	On the user's device (browser, phone, desktop). |	On remote cloud servers. |	On dedicated servers (internal or external).
Common Tech |	HTML, CSS, JavaScript, React, Swift, Flutter. |	Python, Node.js, Java, Go, PostgreSQL, MongoDB. |	REST/gRPC APIs, Docker, Stripe, Twilio, OpenAI.

### 1. The Frontend (What You See)
The frontend is everything a user sees, clicks, and types on their screen. It acts as the HTTP client in a web or mobile app or browser.
- Responsibilities: Rendering layouts, animations, buttons, forms, and validating basic user inputs before sending them off.
- Security Limitation: Because frontend code runs directly on the user's device, anyone can inspect it. Sensitive secrets like database passwords or OpenAI API keys must never live here.

### 2. The Backend (The Brain)
The backend is the unseen engine running on remote servers that powers the application. It acts as the HTTP server that receives requests from the frontend.
- Responsibilities: Checking if a user is logged in, applying business rules (like calculating shipping costs), reading or writing to the database, and securely holding API keys (configurations and environments).
- Communication: The frontend never talks directly to the database. Instead, the frontend sends an API request to the backend, and the backend fetches the data safely.

### 3. Services (The Specialists)
As applications grow, putting all backend logic into one giant program becomes hard to maintain. Developers break specific tasks out into independent services, which communicate with the main backend via APIs.
- Internal Microservices: Dedicated pieces of your own system built for one job, such as an Authentication Service for logins, a Notification Service for alerts, generating tokens with auto refresh mechanism, or a Search Service.
- External (Third-Party) Services: Specialized tools built by other companies that your backend calls over the internet, such as Stripe for payments, Twilio for SMS, or OpenAI for AI responses.

### How They Work Together in Real Life?
Imagine clicking "Checkout" in an online shopping app:
1. Frontend: You click the "Pay Now" button on your phone. The frontend sends your cart details to your backend API.
2. Backend: Your server receives the request, checks inventory in its database, and calculates the final total.
3. Services: Your backend calls an external Payment Service to charge your card, then calls an internal Email Service to send your receipt.
4. Frontend: Your backend tells the frontend the order succeeded, and your screen updates to show "Order Confirmed."

# REST APIs 🌐

### REST API stands for REpresentational State Transfer Application Programming Interface.

Think of a restaurant waiter.
- You (customer) request food.
- The waiter (API) takes your order.
- The kitchen (backend) prepares it.
- The waiter brings your food (response).

A REST API allows two applications to communicate over HTTP.

### Common HTTP Methods:
Method |	Purpose |	Example
:--- |:--- | :---
GET |	Retrieve data |	Get user details
POST |	Create data |	Create a new user
PUT |	Replace existing data |	Update user profile
PATCH |	Partially update data	| Update email
DELETE |	Delete data |	Delete user account

### Example:
```
GET /api/users/007
```

### Response:
```json
{
  "id": 007,
  "name": "Kirankumar Yadav",
  "role": "AI ML Engineer"
}
```

# FastAPI ⚡

### FastAPI is a modern, fast, high-performance web framework for building APIs with Python.

Think of it like a highly efficient waiter in a restaurant:  
- You (client) make a request.  
- FastAPI (waiter) validates and processes your request quickly.  
- The backend (kitchen) prepares the response.  
- FastAPI delivers the response back to you.  

FastAPI automatically generates interactive API documentation and ensures data validation, making it easier and safer to build robust APIs.

### Common FastAPI Methods:
Method | Purpose | Example
:--- | :--- | :---
`@app.get()` | Retrieve data | `@app.get("/users/{user_id}")`  
`@app.post()` | Create data | `@app.post("/users/")`  
`@app.put()` | Replace existing data | `@app.put("/users/{user_id}")`  
`@app.patch()` | Partially update data | `@app.patch("/users/{user_id}")`  
`@app.delete()` | Delete data | `@app.delete("/users/{user_id}")`  

### Example:
```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/users/{user_id}")
def get_user(user_id: int):
    return {"id": user_id, "name": "Kirankumar Yadav"}

@app.post("/users/")
def create_user(name: str):
    return {"id": 007, "name": name}
```

# HTTP and Status Codes 📡

### HTTP stands for Hypertext Transfer Protocol.
- It defines how clients and servers communicate.
- HTTP status codes tell us whether a request succeeded, failed, or needs further action.

### Important HTTP Status Codes:
Code |	Meaning |	Simple Explanation
:--- | :--- | :---
200 |	OK |	Request successful
201 |	Created |	New resource created
204 |	No Content |	Successful, but no response body
400 |	Bad Request |	Invalid request
401 |	Unauthorized |	Authentication required or invalid
403 |	Forbidden |	You don't have permission
404 |	Not Found |	Resource doesn't exist
409 |	Conflict |	Request conflicts with existing data
429 |	Too Many Requests |	Too many requests sent
500 |	Internal Server Error |	Server encountered an error
503 |	Service Unavailable |	Server temporarily unavailable

### Real-Life Example:
Imagine accessing an employee portal.
- Login successful: 200
- Invalid input: 400
- Not logged in: 401
- No permission to view salary: 403
- Employee record doesn't exist: 404

### HTTP status codes communicate the result of a request. 

# Streaming With SSE 📺

### SSE stands for Server-Sent Events.
- It allows a server to continuously send updates to a client over a single HTTP connection.
- Imagine watching a live cricket score.
- Instead of refreshing the page every second, the application automatically receives updates when the score changes.

### Example:
An AI chatbot generates a response:
```
Artificial Intelligence is a technology that...
```
Instead of waiting for the entire response, the chatbot displays words progressively as they arrive.

### Common Applications:
- ChatGPT-style streaming responses.
- Live notifications.
- Real-time dashboards.
- Live stock price updates.
- Background task progress.

### HTTP vs SSE:
HTTP |	SSE
:--- | :---
Request and response |	Server continuously sends events
Usually one response |	Multiple updates over one connection
Client requests data |	Server pushes updates

### SSE is useful when the server needs to continuously send updates to the client.

# WebSockets 🔌

### WebSockets provide continuous, two-way communication between a client and a server.
- Imagine a telephone conversation.
- Both people can speak and listen at any time.
- Similarly, WebSockets allow both the frontend and backend to send messages whenever needed.

### Example:
In a real-time chat application:
- User A sends a message. The backend receives it.
- The backend immediately delivers it to User B.
- User B can reply without refreshing the page.

### Applications:
- Live chat applications.
- Multiplayer gaming.
- Real-time collaboration.
- Trading platforms.
- Live monitoring systems.

### SSE vs WebSockets:
SSE	| WebSockets
:--- | :---
Primarily server to client | Two-way communication
Uses HTTP |	Uses WebSocket protocol
Good for live updates |	Good for interactive communication
Simpler for one-way streaming |	Better for bidirectional messaging

### SSE is like watching a live broadcast. WebSockets are like having a telephone conversation.

# Authentication With JWT 🔐

### JWT stands for JSON Web Token.
- It is a token format commonly used to securely communicate authentication and authorization information.
- Imagine entering an office building.
- You show your identity card at the entrance. Once verified, you receive a visitor pass.
- You use that pass to access permitted areas / ODCs. JWT works similarly.

### How It Works?
1. User enters username and password.
2. Backend verifies the credentials.
3. Backend generates a JWT.
4. Client stores the token securely.
5. Client sends the token with subsequent requests.
6. Backend verifies the token before granting access.

### Example JWT Request:
```
GET /api/profile
Authorization: Bearer <JWT_TOKEN>
```

A JWT typically contains three parts:
```
Header.Payload.Signature
```
- Header: Token type and signing algorithm.
- Payload: Claims such as user ID and expiration.
- Signature: Helps verify token integrity.

### Important: 
- JWT payloads are generally encoded, not encrypted.
- Never put passwords or sensitive secrets inside them.
- JWT acts like a digitally signed identity pass.

# Encoding 💬

Imagine you want to send a message to your friend. 
- Convert your message into another format so a computer or system can understand or process it.
- Its primary purpose is to make data easier to store, transmit, or process across different systems.
- Encoding changes the representation of data, not its secrecy.

### Example:
Suppose you have a text:
```
Hello
```
You convert it into Base64:
```
SGVsbG8=
```
Anyone who knows the Base64 decoding rules can convert it back. No secret key or password is required.
```
SGVsbG8=  →  Hello
```

### Python
```python
import base64

message = "Hello World"

# Encoding
encoded = base64.b64encode(
    message.encode("utf-8")
)

print("Encoded:", encoded.decode())

# Decoding
decoded = base64.b64decode(
    encoded
).decode("utf-8")

print("Decoded:", decoded)
```
Output:
```
Encoded: SGVsbG8gV29ybGQ=
Decoded: Hello World
```

### Common Encoding Techniques:
Encoding |	Purpose
:--- | :---
Base64 |	Converts binary data into text representation
UTF-8 |	Represents text characters as bytes
ASCII |	Represents basic characters using numeric codes
URL Encoding |	Makes data safe to include in URLs
Hex Encoding |	Represents bytes using hexadecimal characters

### Where Is Encoding Used?
- Sending images through APIs.
- Representing text in different formats.
- Transmitting binary data through text-based protocols.
- Encoding special characters in URLs.
- Representing text inside JSON and XML.

# Encryption 🔐
- Lock your message so that only someone with the correct key can read it.
- The process of converting readable data (plaintext) into an unreadable format (ciphertext) using a cryptographic algorithm and a key.
- Its primary purpose is to protect data from unauthorized access. Protects data by making it unreadable without the appropriate key.

### Example:
Suppose you have this message:
```
Hello
```
You encrypt it using an encryption algorithm and a secret key.
```
X7@pL9#qT2
```
Someone who intercepts this encrypted message cannot normally understand it.

### Python
```python
from cryptography.fernet import Fernet

# Generate a secret key
key = Fernet.generate_key()

cipher = Fernet(key)

message = b"Hello World"

# Encryption
encrypted = cipher.encrypt(message)

print("Encrypted:", encrypted)

# Decryption
decrypted = cipher.decrypt(encrypted)

print("Decrypted:", decrypted.decode())
```
Output:
```
Encrypted: gAAAAAB... (encrypted data)
Decrypted: Hello World
```

To retrieve the original message, the authorized recipient needs the appropriate decryption key.
```
Plaintext
    |
    v
Encryption + Key
    |
    v
Ciphertext
    |
    v
Decryption + Key
    |
    v
Original Plaintext
```

### Common Encryption Algorithms:
Algorithm |	Purpose
:--- | :---
AES |	Advanced Encryption Standard - Symmetric encryption
RSA |	Rivest Shamir Adleman - Asymmetric cryptography
ChaCha20 |	Symmetric encryption
ECC |	Elliptic Curve Cryptography, commonly used for key agreement and digital signatures

### Where Is Encryption Used?
- Online banking.
- Secure messaging applications.
- HTTPS websites.
- Password managers.
- Cloud storage security.
- Protecting sensitive customer information.

# Hashing 🧩
- Hashing converts input data into a fixed-length hash value using a hash function.
- Unlike encoding and encryption, hashing is designed to be one-way.
- Passwords should be stored using dedicated password-hashing algorithms such as Argon2id, bcrypt, or scrypt, not plain SHA-256.

### Example:
```
Input: Hello
SHA-256 Hash: 185f8db32271fe25f561a6fc938b2e264306ec304eda518007d1764826381969
```
You cannot practically reverse a secure hash to retrieve the original input.

### Where Is Hashing Used?
- Password storage using Argon2 or bcrypt.
- File integrity verification.
- Digital signatures.
- Data deduplication.
- Content identification.

# Encoding vs Encryption vs Hashing:

### Encoding = Translation (Changes how data is represented.)
Converting English into another language or format so it can be understood using known rules.

### Encryption = Locking (Protects data from unauthorized reading.)
Locking a message so only someone with the appropriate key can read it.

### Hashing = Fingerprinting (Creates a one-way fingerprint of data.)
Creating a unique-looking fingerprint of data that cannot practically be reversed.

# OAuth 2.0 🔑
- OAuth 2.0 is an authorization framework that allows an application to access resources on another service with permission.
- Imagine giving a delivery person permission to collect a package from your apartment reception.
- You don't give them your house keys. You provide limited permission for a specific task.
- OAuth 2.0 is about granting permission to access resources without sharing your password.

### Real-Life Example:
You open an application and click:
> Sign in with Google.

The application redirects you to Google.
- You approve the requested permissions.
- Google provides the application with the appropriate authorization credentials.
- The application can then access permitted resources.

### Common Use Cases:
- Google Login integrations.
- Microsoft account integrations.
- Third-party application access.
- Accessing Google Drive.
- Accessing external APIs.

### JWT vs OAuth 2.0:
JWT	| OAuth 2.0
:--- | :---
Token format |	Authorization framework
Represents claims |	Defines authorization flows
Can carry identity information |	Enables delegated access
Can be used as an access token |	May use JWT or opaque access tokens

# SQL vs NoSQL 🗄️

These are two major categories of database systems.

Imagine organizing information in a company.
- SQL: Information is organized into structured tables.
- NoSQL: Information can be organized into flexible structures such as documents, key-value pairs, or graphs.
- SQL is generally table-oriented. NoSQL supports multiple data models.

### SQL Databases:
- PostgreSQL
- MySQL
- Microsoft SQL Server
- Oracle Database

### Example Table:
ID | Name	| Department
:--- | :--- | :---
101 |	Kirankumar |	AI
102 |	Suraj	| DevOps
103 |	Sumit |	Engineering

### NoSQL Databases:
- MongoDB
- Redis
- Cassandra
- DynamoDB

### Example MongoDB document:
```json
{
  "id": 101,
  "name": "Kirankumar",
  "skills": [
    "AI",
    "ML",
    "GenAI"
  ]
}
```

### SQL vs NoSQL:
Feature |	SQL |	NoSQL
:--- | :--- | :---
Structure |	Tables |	Documents, key-value, etc.
Schema |	Generally predefined |	Often flexible
Relationships |	Strong relational support |	Depends on database type
Transactions |	Strong support |	Varies by database

### When To Use What?
- SQL: Banking, financial transactions, employee management.
- NoSQL: Product catalogs, event data, flexible application data.

# Database Indexing 🔍

Database indexing helps retrieve data faster.
- Imagine a book containing 1,000 pages. If you want to find a topic, you could read every page.
- Alternatively, you could use the index at the back of the book to find the exact page.
- Indexing helps databases find information faster, just like a book index.

### Without Indexing:
The database might scan thousands or millions of records to find the required information.

### With Indexing:
The database uses an additional data structure to locate matching records more efficiently.

### Example:
```sql
CREATE INDEX idx_users_email
ON users(email);
```

Now queries filtering by email can potentially execute faster:
```sql
SELECT *
FROM users
WHERE email = 'iamkirankumaryadav@gmail.com';
```

### Advantages:
- Faster data retrieval.
- Improved query performance.
- Efficient filtering and searching.

### Disadvantages:
- Requires additional storage.
- Can slow down INSERT, UPDATE, and DELETE operations.
- Requires index maintenance.

### Transactions and ACID 💳

A database transaction is a group of operations treated as one logical unit of work.

Imagine transferring ₹1,000 from Account A to Account B.

Two operations must happen:
1. Deduct ₹1,000 from Account A.
2. Add ₹1,000 to Account B.

What happens if money is deducted from A but not added to B?
- Transactions help ensure that the operations are handled reliably.
- If something goes wrong before committing, the transaction can be rolled back.
- ACID ensures reliable database transactions.

### ACID Properties:
Property |	Meaning |	Simple Explanation
:--- | :--- | :---
Atomicity |	All or Nothing |	Both operations succeed or neither does
Consistency |	Valid State |	Database rules remain satisfied
Isolation |	Independent Execution |	Concurrent transactions don't improperly interfere
Durability | Permanent Changes | Committed changes survive failures

### Example:
```sql
BEGIN;

UPDATE accounts
SET balance = balance - 1000
WHERE id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE id = 2;

COMMIT;
```

# Caching With Redis ⚡

Caching means storing frequently accessed data temporarily so that it can be retrieved faster.
- Redis is an in-memory data store commonly used for caching.
- Redis reduces repeated database work and improves response speed.

### Example:
Suppose an AI application frequently retrieves product information.

### Without caching:
1. User requests product information.
2. Backend queries the database.
3. Database returns the result.
4. Backend sends the response.

### With Redis:
1. User requests product information.
2. Backend checks Redis.
3. If the information exists, Redis returns it immediately.
4. Otherwise, backend queries the database and may store the result in Redis.

### Common Applications:
- API response caching.
- User sessions.
- Frequently accessed database records.
- Rate limiting.
- Real-time counters.

# Message Queues 📨

A message queue allows applications to communicate by sending messages that can be processed later.
- Imagine a restaurant during lunchtime. Customers place orders.
- Instead of preparing every order instantly, the restaurant puts orders into a queue and processes them one by one.
- Message queues help applications communicate and process work asynchronously.

### Example:
An e-commerce application receives an order. It needs to:
1. Save the order.
2. Send a confirmation email.
3. Update inventory.
4. Notify the delivery team.
Instead of doing everything within the user's request, the backend can place tasks into a message queue.

### Popular Message Queue Technologies:
- RabbitMQ
- Apache Kafka
- Amazon SQS
- Redis Streams

# Background Jobs ⚙️

Background jobs are tasks that run separately from the main user request.
- Imagine uploading a large video.
- You don't want the application to freeze while the video is processed.
- Instead, the application accepts the upload and processes the video in the background.
- Background jobs allow long-running tasks to execute without making users wait.
- Rate limiting controls how frequently clients can use your API.

# Rate Limiting 🚦

Rate limiting controls how many requests a user or client can make within a specified period.
- Imagine a supermarket with a limited number of customers allowed inside at once. This prevents overcrowding.
- Rate limiting protects APIs from excessive requests.

### Example:
An API allows:
- Maximum 100 requests per user per minute.
- If a user sends 101 requests within one minute, the additional request may be rejected.
- The server commonly responds with:
```
429 Too Many Requests
```

### Why Is It Important?
- Prevents API abuse.
- Protects backend resources.
- Reduces excessive traffic.
- Helps control infrastructure costs.
- Protects AI APIs from expensive repeated calls.

### Popular Implementation Tools:
- Redis
- API Gateway
- NGINX
- Cloudflare

### Examples:
- Sending emails.
- Generating PDF reports.
- Processing uploaded images.
- Running ML model inference.
- Generating embeddings.
- Processing large datasets.
- Scheduling periodic tasks.

### Example Workflow:
```
User Submits Request
        |
        v
Backend Accepts Request
        |
        v
Task Added To Queue
        |
        v
Background Worker
        |
        v
Task Processing
        |
        v
Task Completed
```

### Popular Tools:
- Celery (Python)
- RQ (Python)
- BullMQ (Node.js)
- Sidekiq (Ruby)

### Message Queue vs Background Jobs:
- Message queue: Stores and distributes messages.
- Background job: The actual task that needs to be executed.

# Idempotency Keys 🔁

Idempotency means performing the same operation multiple times produces the same final result as performing it once.
- Imagine clicking a payment button twice because the first click appeared unresponsive.
- You don't want to be charged twice!
- An idempotency key helps prevent duplicate processing of the same request.
- Idempotency keys help prevent duplicate operations when requests are retried.

### Example:
A payment request includes:
```http
POST /api/payments
Idempotency-Key: payment-12345
```

### The backend:
1. Checks whether the key has already been processed.
2. If it has, returns the previously stored result.
3. If it hasn't, processes the payment.
4. Stores the result against the key.
If the same request is sent again with the same key, the payment is not processed a second time.

### Where Is It Used?
- Payment processing.
- Order creation.
- Booking systems.
- Financial transactions.
- External API integrations.

# Retries With Backoff ⏳

Sometimes an API request fails because a service is temporarily unavailable.
- Instead of immediately giving up, the application can retry the request.
- However, retrying continuously can overload the service.
- Backoff means waiting progressively longer between retry attempts.
- Retry with backoff gives temporarily failing services time to recover.

Imagine calling someone who is busy.
- First attempt: Wait 1 second.
- Second attempt: Wait 2 seconds.
- Third attempt: Wait 4 seconds.
- Fourth attempt: Wait 8 seconds.

Example:
```python
import time

for attempt in range(4):
    try:
        call_api()
        break

    except Exception:
        wait_time = 2 ** attempt
        time.sleep(wait_time)
```
In production, you should also use maximum retry limits, and appropriate error classification.

### Where Is It Used?
- External API calls.
- LLM API requests.
- Database connections.
- Distributed systems.
- Cloud service integrations.

# File Uploads to S3 ☁️

### Amazon S3 stands for Amazon Simple Storage Service. 
S3 stores files separately from your application's database.

It is an object storage service used to store files such as:
- Images.
- Videos.
- PDFs.
- Documents.
- Audio files.
- ML datasets.

Imagine a huge digital warehouse where applications can store and retrieve files.

### Example:
Suppose a user uploads a PDF to an AI-powered document assistant. The workflow:
1. User uploads a PDF.
2. Backend validates the file.
3. Backend uploads the file to S3.
4. S3 stores the file.
5. Backend saves the file location in the database.
6. AI processing retrieves the file when needed.

### Important S3 Concepts:
Term |	Meaning
:--- | :---
Bucket |	Container for storing objects
Object |	Stored file
Key |	Unique object identifier within a bucket
Presigned URL |	Temporary URL granting specified access
Versioning |	Maintains different versions of objects

# Pagination 📄

Pagination means dividing large amounts of data into smaller pages.
- Imagine reading a 1,000-page book.
- Instead of displaying every page at once, you read 20 pages at a time.
- Web applications use pagination to display large datasets efficiently.
- Pagination prevents applications from retrieving and displaying too much data at once.

### Example:
Suppose an application contains 10,000 employee records.

Instead of returning all records:
```
GET /api/employees?page=1&limit=20
```

This returns the first 20 records.

Next request:
```
GET /api/employees?page=2&limit=20
```
This returns the next 20 records.

### Common Pagination Types:
Type |	Explanation
:--- | :---
Offset Pagination |	Uses page number or offset
Cursor Pagination |	Uses a reference to the last retrieved record
Keyset Pagination |	Uses indexed ordering fields to retrieve the next records

### Where Is It Used?
- E-commerce product listings.
- Social media feeds.
- Employee directories.
- Transaction histories.
- Search results.

# Pydantic? 🎯

### Pydantic is a Python library used for data validation, parsing, and serialization.
- In simple terms, Pydantic acts like a quality checkpoint for data entering your application.
- Pydantic uses Python type hints and validation rules to define the expected structure of data.
- FastAPI uses Pydantic models to validate API request bodies automatically.

It checks whether incoming data:
- Has the expected fields.
- Contains the correct data types.
- Follows specified validation rules.
- Meets required constraints.

If the data is invalid, Pydantic provides meaningful validation errors.

### Popular Use Cases:
- FastAPI application development.
- REST API request validation.
- Configuration management.
- LLM structured outputs.
- Data processing pipelines.
- AI Agent input and output validation.

### Example:
```python
pip install pydantic email-validator
from pydantic import BaseModel, EmailStr, Field

class Employee(BaseModel):
    name: str
    age: int = Field(gt=18)
    email: EmailStr
```

Here:
Component |	Meaning
:--- | :---
BaseModel |	Base class used to define data models
name: | str	Name must be a string
age: | int	Age must be an integer
Field(gt=18) |	Age must be greater than 18
EmailStr |	Email must have a valid email format

### Pass Valid Data
```python
employee = Employee(
    name="Kiran",
    age=30,
    email="kiran@example.com"
)

print(employee)
```
Output:
```
name='Kiran' age=30 email='kiran@example.com'
```

### Pass Invalid Data
```python
employee = Employee(
    name="Kiran",
    age=15,
    email="invalid-email"
)
```
Pydantic raises a `ValidationError` because:
- Age is not greater than 18.
- Email is invalid.
This means invalid data is caught before your application uses it.

### Pydantic in GenAI and Agentic AI
Pydantic is particularly useful when building LLM-powered applications. 

LLMs can sometimes generate responses with:
- Missing fields.
- Incorrect data types.
- Unexpected structures.
- Invalid values.

Pydantic helps validate the structure of the generated response before passing it to the next component.

# Logging and Monitoring 📊

### Logging and monitoring help developers understand what is happening inside an application.

Imagine driving a car.
- Dashboard indicators show current speed and fuel.
- Event records help identify what happened during a journey.

Backend applications need similar visibility.

### Logging records events that happen inside an application.

Example:
```
INFO: User logged in successfully.
WARNING: API response is slow.
ERROR: Database connection failed.
```

### Monitoring continuously tracks the health and performance of an application.

### Common Metrics:
- CPU Utilization.
- Memory Usage.
- API Response Time.
- Request Count.
- Error Rate.
- Database Performance.
- Queue Processing Time.

### Popular Tools:
Category |	Tools
:--- | :---
Logging |	ELK Stack, Loki
Monitoring |	Prometheus
Dashboards |	Grafana
Application Monitoring |	Datadog, New Relic
Error Tracking |	Sentry
Distributed Tracing |	OpenTelemetry

Example: Suppose your AI application takes 30 seconds to generate a response.

Monitoring can help identify whether the delay comes from:
- Slow database queries.
- External LLM API latency.
- Network problems.
- Insufficient infrastructure.
- Slow background processing.

### Logging tells you what happened. Monitoring tells you how your system is performing.
