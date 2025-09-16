# HTTP Status Codes Guide

## What are HTTP Status Codes?

HTTP status codes are 3-digit numbers that web servers send back to clients (browsers, apps, APIs) to communicate the result of a request. Think of them as the server's way of saying "here's what happened with your request."

## Status Code Categories

Status codes are organized into 5 main categories based on their first digit:

| Category | Range | Meaning |
|----------|-------|---------|
| 1xx | 100-199 | Informational responses |
| 2xx | 200-299 | Success |
| 3xx | 300-399 | Redirection |
| 4xx | 400-499 | Client errors |
| 5xx | 500-599 | Server errors |

---

## 1xx - Informational Responses

These are rarely seen by end users but are used for protocol-level communication.

### 100 Continue
- **Meaning**: Server received initial part of request, client should continue
- **When you see it**: Rarely, mostly in large file uploads
- **Example**: Uploading a large video file

### 101 Switching Protocols
- **Meaning**: Server is switching to a different protocol
- **When you see it**: WebSocket connections, HTTP/2 upgrades

---

## 2xx - Success Responses ✅

These indicate that the request was received, understood, and processed successfully.

### 200 OK
- **Meaning**: Everything worked perfectly
- **When you see it**: Normal webpage loads, successful API calls
- **Example**: Loading Google.com homepage

### 201 Created
- **Meaning**: Request succeeded and a new resource was created
- **When you see it**: Creating a new user account, posting a new blog article
- **Example**: Signing up for a new service

### 202 Accepted
- **Meaning**: Request accepted for processing, but not completed yet
- **When you see it**: Background jobs, async operations
- **Example**: Uploading a video that needs processing

### 204 No Content
- **Meaning**: Success, but no content to return
- **When you see it**: DELETE operations, saving settings
- **Example**: Deleting a file successfully

---

## 3xx - Redirection Responses 🔄

These indicate that further action is needed to complete the request.

### 301 Moved Permanently
- **Meaning**: Resource has permanently moved to a new URL
- **When you see it**: Website restructuring, domain changes
- **Example**: Old company website redirecting to new domain

### 302 Found (Temporary Redirect)
- **Meaning**: Resource temporarily located at different URL
- **When you see it**: Temporary maintenance pages, A/B testing
- **Example**: Redirecting to mobile version of site

### 304 Not Modified
- **Meaning**: Resource hasn't changed since last request
- **When you see it**: Browser caching, faster page loads
- **Example**: Revisiting a page that hasn't been updated

### 307 Temporary Redirect
- **Meaning**: Like 302, but method must not change
- **When you see it**: Modern alternative to 302
- **Example**: API endpoint temporary redirect

---

## 4xx - Client Error Responses ❌

These indicate that the client (you) made an error in the request.

### 400 Bad Request
- **Meaning**: Server couldn't understand the request
- **When you see it**: Malformed URLs, invalid data
- **Example**: Submitting a form with invalid email format

### 401 Unauthorized
- **Meaning**: Authentication required or failed
- **When you see it**: Need to log in, expired session
- **Example**: Trying to access your bank account without logging in

### 403 Forbidden
- **Meaning**: Server understood request but refuses to authorize it
- **When you see it**: Insufficient permissions, blocked access
- **Example**: Trying to access admin panel as regular user

### 404 Not Found
- **Meaning**: Requested resource doesn't exist
- **When you see it**: Broken links, deleted pages, typos in URL
- **Example**: Clicking on an old bookmark that no longer exists

### 405 Method Not Allowed
- **Meaning**: HTTP method not supported for this resource
- **When you see it**: Using POST where only GET is allowed
- **Example**: Trying to POST to a read-only API endpoint

### 409 Conflict
- **Meaning**: Request conflicts with current server state
- **When you see it**: Trying to create duplicate resources
- **Example**: Registering with an email that already exists

### 422 Unprocessable Entity
- **Meaning**: Request was well-formed but contains semantic errors
- **When you see it**: Validation failures in APIs
- **Example**: Password doesn't meet complexity requirements

### 429 Too Many Requests
- **Meaning**: Rate limit exceeded
- **When you see it**: Making too many API calls too quickly
- **Example**: Refreshing a page too many times

---

## 5xx - Server Error Responses 💥

These indicate that the server failed to fulfill a valid request.

### 500 Internal Server Error
- **Meaning**: Generic server error, something went wrong
- **When you see it**: Server bugs, crashes, misconfigurations
- **Example**: Database connection failure

### 501 Not Implemented
- **Meaning**: Server doesn't support the functionality required
- **When you see it**: Unsupported HTTP methods or features
- **Example**: Server doesn't support HTTP/3

### 502 Bad Gateway
- **Meaning**: Server acting as gateway received invalid response
- **When you see it**: Load balancer issues, proxy problems
- **Example**: Web server can't reach database server

### 503 Service Unavailable
- **Meaning**: Server temporarily unable to handle requests
- **When you see it**: Maintenance mode, server overload
- **Example**: Website down for scheduled maintenance

### 504 Gateway Timeout
- **Meaning**: Server acting as gateway didn't receive timely response
- **When you see it**: Slow backend services, network issues
- **Example**: Payment gateway taking too long to respond

---

## Quick Reference Table

| Code | Status | Common Cause |
|------|--------|--------------|
| 200 | OK | Normal successful request |
| 301 | Moved Permanently | URL changed forever |
| 400 | Bad Request | Invalid request format |
| 401 | Unauthorized | Need to authenticate |
| 403 | Forbidden | No permission to access |
| 404 | Not Found | Resource doesn't exist |
| 429 | Too Many Requests | Rate limited |
| 500 | Internal Server Error | Server-side bug |
| 502 | Bad Gateway | Proxy/gateway issue |
| 503 | Service Unavailable | Server temporarily down |

---

## Best Practices for Developers

### When Building APIs:
- Use appropriate status codes for different scenarios
- Be consistent across your API endpoints
- Include helpful error messages in response body
- Use 201 for resource creation, not just 200

### When Handling Errors:
- Implement proper error handling for each status code category
- Show user-friendly messages instead of raw status codes
- Log detailed error information for debugging
- Implement retry logic for 5xx errors

### Common Patterns:
```
GET request successful → 200
POST creating resource → 201
PUT/PATCH updating → 200 or 204
DELETE successful → 204 or 200
Validation failed → 400 or 422
Not authenticated → 401
Not authorized → 403
Resource not found → 404
```

---

## Real-World Examples

### E-commerce Website:
- Browsing products: **200 OK**
- Adding item to cart: **201 Created** or **200 OK**
- Checking out without login: **401 Unauthorized**
- Trying to buy out-of-stock item: **409 Conflict**
- Payment processing error: **500 Internal Server Error**

### Social Media Platform:
- Loading timeline: **200 OK**
- Creating new post: **201 Created**
- Editing someone else's post: **403 Forbidden**
- Viewing deleted post: **404 Not Found**
- Posting too frequently: **429 Too Many Requests**

---

## Remember:
- 2xx = Success 😊
- 3xx = Redirect 🔄
- 4xx = Your fault 😅
- 5xx = Server's fault 💥

Status codes are the foundation of HTTP communication - understanding them will make you a better developer and help you debug issues more effectively!
