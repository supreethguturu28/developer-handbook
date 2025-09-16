# HTTP Methods Guide

## Overview

HTTP methods (also called HTTP verbs) define the action to be performed on a resource. They tell the server what operation the client wants to execute. Understanding HTTP methods is crucial for RESTful API design and web development.

## Table of Contents

1. [Quick Reference](#quick-reference)
2. [Main HTTP Methods](#main-http-methods)
3. [Less Common Methods](#less-common-methods)
4. [Method Properties](#method-properties)
5. [RESTful API Usage](#restful-api-usage)
6. [Best Practices](#best-practices)
7. [Common Scenarios](#common-scenarios)
8. [Examples](#examples)

## Quick Reference

| Method | Purpose | Safe | Idempotent | Has Body | Common Use |
|--------|---------|------|------------|----------|------------|
| `GET` | Retrieve data | ✅ | ✅ | ❌ | Fetch resources |
| `POST` | Create/Submit data | ❌ | ❌ | ✅ | Create new resources |
| `PUT` | Update/Replace | ❌ | ✅ | ✅ | Update entire resource |
| `PATCH` | Partial update | ❌ | ❌ | ✅ | Update part of resource |
| `DELETE` | Remove resource | ❌ | ✅ | ❌ | Delete resources |
| `HEAD` | Get headers only | ✅ | ✅ | ❌ | Check if resource exists |
| `OPTIONS` | Get allowed methods | ✅ | ✅ | ❌ | CORS preflight |

## Main HTTP Methods

### GET
**Purpose**: Retrieve data from the server

```http
GET /api/users/123 HTTP/1.1
Host: example.com
```

**Characteristics**:
- ✅ Safe (doesn't modify server state)
- ✅ Idempotent (same result every time)
- ❌ No request body
- ✅ Cacheable
- ✅ Can be bookmarked

**Use Cases**:
- Fetch user profiles
- Get list of products
- Retrieve blog posts
- Download files

---

### POST
**Purpose**: Submit data to create new resources or trigger actions

```http
POST /api/users HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com"
}
```

**Characteristics**:
- ❌ Not safe (modifies server state)
- ❌ Not idempotent (multiple calls create multiple resources)
- ✅ Can have request body
- ❌ Not cacheable
- ❌ Cannot be bookmarked

**Use Cases**:
- Create new user accounts
- Submit forms
- Upload files
- Process payments
- Send emails

---

### PUT
**Purpose**: Update or replace an entire resource

```http
PUT /api/users/123 HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "id": 123,
  "name": "John Smith",
  "email": "johnsmith@example.com",
  "age": 30
}
```

**Characteristics**:
- ❌ Not safe (modifies server state)
- ✅ Idempotent (same result when called multiple times)
- ✅ Can have request body
- ❌ Not cacheable

**Use Cases**:
- Update entire user profile
- Replace configuration settings
- Update complete product information

---

### PATCH
**Purpose**: Apply partial updates to a resource

```http
PATCH /api/users/123 HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "email": "newemail@example.com"
}
```

**Characteristics**:
- ❌ Not safe (modifies server state)
- ❌ Not idempotent (depends on implementation)
- ✅ Can have request body
- ❌ Not cacheable

**Use Cases**:
- Update specific fields
- Change user preferences
- Modify part of a document

---

### DELETE
**Purpose**: Remove a resource from the server

```http
DELETE /api/users/123 HTTP/1.1
Host: example.com
```

**Characteristics**:
- ❌ Not safe (modifies server state)
- ✅ Idempotent (deleting same resource multiple times has same effect)
- ❌ Usually no request body
- ❌ Not cacheable

**Use Cases**:
- Delete user accounts
- Remove blog posts
- Clear cache entries

---

### HEAD
**Purpose**: Get response headers without the body

```http
HEAD /api/users/123 HTTP/1.1
Host: example.com
```

**Characteristics**:
- ✅ Safe (doesn't modify server state)
- ✅ Idempotent
- ❌ No request body
- ❌ No response body (headers only)

**Use Cases**:
- Check if resource exists
- Get metadata (content length, last modified)
- Validate cache
- Check server capabilities

---

### OPTIONS
**Purpose**: Get allowed methods and CORS information

```http
OPTIONS /api/users HTTP/1.1
Host: example.com
```

**Characteristics**:
- ✅ Safe
- ✅ Idempotent
- ❌ Usually no request body

**Use Cases**:
- CORS preflight requests
- Discover allowed methods
- API capability discovery

## Less Common Methods

### CONNECT
- Creates a tunnel to the server (used for HTTPS through proxies)

### TRACE
- Performs a message loop-back test (rarely used, often disabled for security)

## Method Properties

### Safe Methods
Methods that don't modify server state:
- `GET`, `HEAD`, `OPTIONS`

### Idempotent Methods
Methods that produce the same result when called multiple times:
- `GET`, `HEAD`, `PUT`, `DELETE`, `OPTIONS`

### Methods with Request Body
Methods that can include data in the request:
- `POST`, `PUT`, `PATCH`

## RESTful API Usage

### CRUD Operations Mapping

| CRUD Operation | HTTP Method | Example |
|----------------|-------------|---------|
| **Create** | POST | `POST /api/users` |
| **Read** | GET | `GET /api/users/123` |
| **Update** | PUT/PATCH | `PUT /api/users/123` |
| **Delete** | DELETE | `DELETE /api/users/123` |

### Resource Collections vs Individual Resources

```http
# Collection operations
GET /api/users           # Get all users
POST /api/users          # Create new user

# Individual resource operations
GET /api/users/123       # Get specific user
PUT /api/users/123       # Update specific user
PATCH /api/users/123     # Partially update user
DELETE /api/users/123    # Delete specific user
```

## Best Practices

### 1. Use Appropriate Methods
```http
# ✅ Good
GET /api/users                    # Retrieve users
POST /api/users                   # Create user
PUT /api/users/123               # Update user
DELETE /api/users/123            # Delete user

# ❌ Bad
GET /api/deleteUser?id=123       # Don't use GET for deletions
POST /api/getUsers               # Don't use POST for retrievals
```

### 2. Respect Idempotency
```http
# ✅ Idempotent - safe to retry
PUT /api/users/123
DELETE /api/users/123

# ❌ Not idempotent - be careful with retries
POST /api/users                  # Creates new user each time
```

### 3. Use Proper Status Codes
```http
# GET responses
200 OK                           # Resource found
404 Not Found                    # Resource doesn't exist

# POST responses
201 Created                      # Resource created successfully
400 Bad Request                  # Invalid data

# PUT responses
200 OK                           # Updated successfully
201 Created                      # Created new resource

# DELETE responses
204 No Content                   # Deleted successfully
404 Not Found                    # Resource didn't exist
```

## Common Scenarios

### 1. User Management API
```http
# Get all users
GET /api/users

# Get specific user
GET /api/users/123

# Create new user
POST /api/users
Content-Type: application/json
{
  "name": "John Doe",
  "email": "john@example.com"
}

# Update user (complete replacement)
PUT /api/users/123
Content-Type: application/json
{
  "id": 123,
  "name": "John Smith",
  "email": "johnsmith@example.com"
}

# Update user email only
PATCH /api/users/123
Content-Type: application/json
{
  "email": "newemail@example.com"
}

# Delete user
DELETE /api/users/123
```

### 2. File Operations
```http
# Check if file exists
HEAD /api/files/document.pdf

# Download file
GET /api/files/document.pdf

# Upload new file
POST /api/files
Content-Type: multipart/form-data

# Replace file
PUT /api/files/document.pdf

# Delete file
DELETE /api/files/document.pdf
```

### 3. Shopping Cart
```http
# View cart
GET /api/cart

# Add item to cart
POST /api/cart/items
{
  "productId": 456,
  "quantity": 2
}

# Update item quantity
PATCH /api/cart/items/789
{
  "quantity": 5
}

# Remove item from cart
DELETE /api/cart/items/789

# Clear entire cart
DELETE /api/cart
```

## Examples

### JavaScript Fetch API
```javascript
// GET request
const users = await fetch('/api/users')
  .then(response => response.json());

// POST request
const newUser = await fetch('/api/users', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    name: 'John Doe',
    email: 'john@example.com'
  })
}).then(response => response.json());

// PUT request
const updatedUser = await fetch('/api/users/123', {
  method: 'PUT',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    id: 123,
    name: 'John Smith',
    email: 'johnsmith@example.com'
  })
}).then(response => response.json());

// PATCH request
await fetch('/api/users/123', {
  method: 'PATCH',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    email: 'newemail@example.com'
  })
});

// DELETE request
await fetch('/api/users/123', {
  method: 'DELETE'
});
```

### cURL Examples
```bash
# GET request
curl -X GET https://api.example.com/users

# POST request
curl -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -d '{"name":"John Doe","email":"john@example.com"}'

# PUT request
curl -X PUT https://api.example.com/users/123 \
  -H "Content-Type: application/json" \
  -d '{"id":123,"name":"John Smith","email":"johnsmith@example.com"}'

# PATCH request
curl -X PATCH https://api.example.com/users/123 \
  -H "Content-Type: application/json" \
  -d '{"email":"newemail@example.com"}'

# DELETE request
curl -X DELETE https://api.example.com/users/123

# HEAD request
curl -I https://api.example.com/users/123

# OPTIONS request
curl -X OPTIONS https://api.example.com/users
```

## Additional Resources

- [MDN HTTP Methods Documentation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
- [RFC 7231 - HTTP/1.1 Semantics](https://tools.ietf.org/html/rfc7231)
- [REST API Tutorial](https://restfulapi.net/)
- [HTTP Status Codes Guide](http-status-codes-guide.md)

---

*Remember: Choose the right HTTP method based on the action you want to perform. When in doubt, follow REST conventions and consider the method's properties (safe, idempotent, cacheable).*