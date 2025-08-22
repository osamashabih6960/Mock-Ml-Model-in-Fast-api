# Mock ML Models

📅 **Date:** Monday, August 22, 2025  
🕒 **Time:** 11:14 PM  

---

## What is meant by Mocking ML Models?

Mocking an ML model means replacing the actual ML model with a **fake (or simulated) object** in your tests that behaves like the real model but doesn't perform any actual computation.  

Instead of loading a large model file and calling its `predict()` method, you **pretend (mock)** that a model exists and will return a known, controlled value.  

---

## Why Mock ML Models?

### 1. ML Models Are Heavy to Load
- In production-grade ML APIs, models may be trained on large datasets and saved as serialized `.pkl`, `.joblib`, or `.h5` files.  
- These files can be **hundreds of MBs or even GBs** in size and may contain complex architectures (e.g., deep learning models).  
- Deserializing and initializing these models can take **several seconds or even minutes**.  
- Running this load operation for every test case makes the test **slow, resource-intensive, and prone to timeouts or memory exhaustion**—not ideal for a CI/CD pipeline.  

---

### 2. Tests Should Focus on API Logic
- When testing an API endpoint (e.g., `/predict`), the goal is to check if the endpoint accepts input and returns a response in the correct format.  
- We **do not care** about whether the prediction itself is accurate.  
- Using a real model introduces unnecessary complexity and **violates unit testing principles**.  

---

### 3. Mocking Makes Tests Fast and Deterministic
- Mocking replaces the actual model object with a **fake object** that simulates the `predict` method.  
- This fake object can:
  - Return **predefined outputs** for known inputs.  
  - Simulate **exceptions** to test error handling.  
  - Avoid real computation, making the test **lightweight and fast**.  
- As a result, tests become **deterministic**: the same input always yields the same response, which helps maintain stability in test results.  

---
## 3.1 - Demo

### 📂 File Structure
main.py
model.py
test_main.py
training.ipynb


### 🔄 Control Flow
- Uses the `patch()` method from `unittest.mock` to mock the real ML model’s `.predict()` method.  
- The mocked method always returns `[99]`.  
- Sends a POST request to the `/predict` endpoint using `TestClient`.  
- Asserts that the endpoint returns a `200 OK` with a prediction of **99**.  
- Ensures that the mocked `.predict()` was called with the expected input.







     

