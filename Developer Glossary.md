# Basic Architecture 🏗️

### Frontend, backend, and services are the core layers of modern software architecture. 
- Frontend: The visual user interface (UI) we interact with (see, click, type, scroll, etc.)
- Backend: The behind-the-scenes engine handling business logic, calculations, and database operations.
- Services: Modular, specialized backend components either built internally or provided by third parties, that perform specific tasks.

### How They Compare
Feature |	Frontend |	Backend |	Services
:--- | :--- | :--- | :---
Also Known As	| Client-side, UI (User Interface). |	Server-side, Core Application. |	Microservices, APIs, Third-Party Integrations.
Primary Role | Displays information and captures user actions. | Processes data, enforces security, and manages databases. |	Executes one focused task (e.g., payments, emails, AI).
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

Example:
```
GET /api/users/007
```

Response:
```json
{
  "id": 007,
  "name": "Kirankumar Yadav",
  "role": "AI ML Engineer"
}
```

# FastAPI ⚡

FastAPI is a modern, fast (high-performance) web framework for building APIs with Python based on standard Python type hints.

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

Example:
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
