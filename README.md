# 🚀 JSONPlaceholder API Performance Test (Apache JMeter)

This project contains a **JMeter performance test plan** for the public demo API **[JSONPlaceholder](https://jsonplaceholder.typicode.com/)**.  
It is designed to simulate high load on simple `GET` endpoints and validate the API responses using **Response Assertions**.

---

## 📁 Project File

- `jsonplaceholder_performance.jmx` – main JMeter Test Plan file

---

## 🛠 Tech Stack

- **Tool:** Apache JMeter 5.6.3
- **Protocol:** HTTPS
- **Base URL:** `https://jsonplaceholder.typicode.com`
- **Implementation:** HttpClient4

---

## 🎯 Test Scenario

The test simulates multiple virtual users sending requests to two JSONPlaceholder endpoints:

1. `GET /users`
2. `GET /posts`

Each user repeatedly sends these requests according to the Thread Group configuration (see below).

---

## 👥 Thread Group Configuration

- **Number of Threads (Users):** `5000`
- **Ramp-Up Period:** `400` seconds  
  → Users are gradually started over 400 seconds.
- **Loop Count:** `100` iterations per user
- **On Sample Error:** `Continue` (errors are logged but test continues)

---

## 🌐 HTTP Configuration

### HTTP Request Defaults

Configured once and reused by all HTTP samplers:

- **Server Name or IP:** `jsonplaceholder.typicode.com`
- **Protocol:** `https`
- **Implementation:** `HttpClient4`

### HTTP Requests

1. **GET users**
   - Method: `GET`
   - Path: `/users`
   - Follow redirects: `true`
   - Keep-Alive: `true`

2. **GET Posts**
   - Method: `GET`
   - Path: `/posts`
   - Follow redirects: `true`
   - Keep-Alive: `true`

---

## ✅ Response Assertions

To ensure the responses are valid, the test uses **Response Assertions**:

1. **Users Response Assertion**
   - Field: **Response Data**
   - Condition: **Contains**
   - Pattern: `"name"`
   - Purpose: Validate that `/users` returns data containing the `name` field.

2. **Posts Response Assertion**
   - Field: **Response Data**
   - Condition: **Contains**
   - Pattern: `"userId"`
   - Purpose: Validate that `/posts` returns data containing the `userId` field.

If an assertion fails, the corresponding sample will be marked as an **error** in the listeners.

---

## 📊 Listeners

The Test Plan includes multiple listeners for analysis:

- **View Results Tree**
  - Inspect individual requests and responses.
  - Check assertion results for each sample.

- **Aggregate Report**
  - Summary metrics (Average, Min, Max, 90% Line, Error %, Throughput, etc.).

- **Aggregate Graph**
  - Visual representation of performance metrics.

- **Assertion Results**
  - Focused view of all assertion successes/failures.

---

## ▶️ How to Run

1. **Install JMeter**  
   - Download from the official Apache JMeter website.
   - Extract and run `jmeter` (GUI mode).

2. **Open the Test Plan**
   - `File` → `Open` → select `jsonplaceholder_performance.jmx`.

3. **(Optional) Adjust the Load**
   - Open **Thread Group**.
   - Edit:
     - **Number of Threads (users)**
     - **Ramp-Up Period**
     - **Loop Count**

4. **Run the Test**
   - Click the **Start** button (green ▶️ icon).

5. **View Results**
   - Open **View Results Tree** and **Aggregate Report** to analyze:
     - Response times
     - Errors
     - Assertions
     - Throughput

---

👨‍💻 *Author:* Ahmad El-Manaseer  
📍 *Focus:* QA & Performance Testing 
