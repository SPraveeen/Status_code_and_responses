# Status_code_and_responses

# 📘 HTTP Status Codes and Their Use in APIs (FastAPI)

---

## ✅ 1xx – Informational Responses

| Code | Meaning               | Use Case                                                                 |
|------|------------------------|--------------------------------------------------------------------------|
| **100** | Continue             | Rare in APIs. Server acknowledges headers received; client continues.   |
| **101** | Switching Protocols  | Used when switching protocols (e.g., to WebSocket).                     |

---

## ✅ 2xx – Success

| Code | Meaning               | Use Case                                                                 |
|------|------------------------|--------------------------------------------------------------------------|
| **200** | OK                   | Standard success for GET, PUT, PATCH, DELETE.                            |
| **201** | Created              | New resource created successfully (used with POST).                      |
| **202** | Accepted             | Request accepted for processing, not completed (e.g., async jobs).       |
| **204** | No Content           | Success with no content returned (e.g., DELETE request).                 |

---

## ✅ 3xx – Redirection

| Code | Meaning               | Use Case                                                                 |
|------|------------------------|--------------------------------------------------------------------------|
| **301** | Moved Permanently    | Resource moved to a new URL.                                            |
| **302** | Found (Temp Redirect)| Temporary redirection to another URL.                                   |
| **304** | Not Modified         | Resource hasn't changed; useful for caching.                             |

---

## ✅ 4xx – Client Errors

| Code | Meaning               | Use Case                                                                 |
|------|------------------------|--------------------------------------------------------------------------|
| **400** | Bad Request          | Invalid request (missing fields, wrong data, etc.).                      |
| **401** | Unauthorized         | Auth required or token invalid/missing.                                  |
| **403** | Forbidden            | Authenticated but not permitted to access.                              |
| **404** | Not Found            | Resource doesn't exist.                                                 |
| **405** | Method Not Allowed   | HTTP method not supported for this route.                               |
| **409** | Conflict             | Request conflicts with current state (e.g., duplicate data).            |
| **422** | Unprocessable Entity | Validation error (common in FastAPI schema validation).                 |
| **429** | Too Many Requests    | Rate limit exceeded.                                                    |

---

## ✅ 5xx – Server Errors

| Code | Meaning               | Use Case                                                                 |
|------|------------------------|--------------------------------------------------------------------------|
| **500** | Internal Server Error | Generic server error.                                                   |
| **501** | Not Implemented      | Functionality not supported.                                            |
| **502** | Bad Gateway          | Invalid response from upstream server.                                  |
| **503** | Service Unavailable  | Server temporarily down or overloaded.                                  |
| **504** | Gateway Timeout      | Upstream server didn’t respond in time.                                 |

---

## 🔧 Example in FastAPI

```python
from fastapi import FastAPI, status, HTTPException

app = FastAPI()

@app.get("/items/{item_id}", status_code=status.HTTP_200_OK)
def read_item(item_id: int):
    if item_id != 1:
        raise HTTPException(status_code=status.HTTP_404_NOT_FOUND, detail="Item not found")
    return {"item_id": item_id}
