# 🔗 Simplifai Backend API Test Cases Report

---

# 1️⃣ GET /applications — Retrieve Application List (Authenticated User)

## 📌 Description

Verify that an authenticated user can retrieve the list of applications using a valid Bearer token.

## 🌐 Request

```http
GET /api/applications
Authorization: Bearer <valid_token>
```

## ✅ Expected Result

The API should return **200 OK** and a list of applications belonging to the authenticated user.

## ❌ Actual Result

```json
Status Code: 200 OK

[
  {
    "id": "ead61859-f979-4283-9f95-4a50409216b1",
    "user_id": "a3c38e71-9784-4b8c-81af-9692a2aa8373",
    "type": "Enrollment Agreement",
    "email": "leman.qrb@gmail.com",
    "phone": "+4488866625",
    "status": "documents_uploaded"
  }
]
```

## 🗄️ Database Verification

```sql
SELECT * FROM applications
WHERE id = 'ead61859-f979-4283-9f95-4a50409216b1';
```

**Status:** ✅ PASS

---

# 2️⃣ GET /applications — Without Bearer Token

## 📌 Description

Verify authorization when no Bearer token is provided.

## 🌐 Request

```http
GET /api/applications
```

## ✅ Expected Result

The API should reject the request with **401 Unauthorized**.

## ❌ Actual Result

```json
Status Code: 401 Unauthorized

{
  "success": false,
  "message": "Unauthorized"
}
```

**Status:** ✅ PASS

---

# 3️⃣ POST /applications — Create a New Application

## 📌 Description

Verify that a new application can be created successfully.

## 🌐 Request

```http
POST /api/applications
```

### Body

```json
{
  "type": "My application"
}
```

## ✅ Expected Result

A new application should be created and returned with **201 Created**.

## ❌ Actual Result

```json
Status Code: 201 Created

{
  "id": "ef7a2867-3c5d-4475-aea9-aceb7681ef5d",
  "status": "DRAFT"
}
```

## 🗄️ Database Verification

```sql
SELECT * FROM applications
WHERE id = 'ef7a2867-3c5d-4475-aea9-aceb7681ef5d';
```

**Status:** ✅ PASS

---

# 4️⃣ POST /applications — Invalid Endpoint

## 📌 Description

Verify the API response when an incorrect endpoint is requested.

## 🌐 Request

```http
POST /api/applicatio
```

### Body

```json
{
  "type": "Tests"
}
```

## ✅ Expected Result

The API should return **404 Not Found**.

## ❌ Actual Result

```json
Status Code: 404 Not Found

{
  "success": false,
  "message": "Route not found",
  "path": "/api/applicatio"
}
```

**Status:** ✅ PASS

---

# 5️⃣ POST /applications/submit — Submit an Application

## 📌 Description

Verify that a completed application can be submitted successfully.

## 🌐 Request

```http
POST /api/applications/submit
```

## ✅ Expected Result

The application should be created with **Pending** status.

## ❌ Actual Result

```json
Status Code: 201 Created

{
  "status": "pending"
}
```

**Status:** ✅ PASS

---

# 6️⃣ POST /applications/submit — Without Bearer Token

## 📌 Description

Verify authorization when submitting without authentication.

## 🌐 Request

```http
POST /api/applications/submit
```

## ✅ Expected Result

The API should return **401 Unauthorized**.

## ❌ Actual Result

```json
Status Code: 401 Unauthorized

{
  "success": false,
  "message": "Unauthorized"
}
```

**Status:** ✅ PASS

---

# 7️⃣ GET /applications/{id} — Valid Application ID

## 📌 Description

Verify that a single application can be retrieved using a valid ID.

## 🌐 Request

```http
GET /api/applications/{id}
```

## ✅ Expected Result

The API should return **200 OK** and the requested application.

## ❌ Actual Result

```json
Status Code: 200 OK
```

Application data was returned successfully.

**Status:** ✅ PASS

---

# 8️⃣ GET /applications/{id} — Invalid Application ID

## 📌 Description

Verify API behavior when an invalid application ID is requested.

## 🌐 Request

```http
GET /api/applications/{invalid_id}
```

## ✅ Expected Result

The API should return **404 Not Found**.

## ❌ Actual Result

```json
Status Code: 404 Not Found

{
  "success": false,
  "message": "Application not found"
}
```

**Status:** ✅ PASS

---

# 9️⃣ DELETE /applications/{id} — Valid Application ID

## 📌 Description

Verify that an application can be deleted successfully.

## 🌐 Request

```http
DELETE /api/applications/{id}
```

## ✅ Expected Result

The API should delete the application and return **204 No Content**.

## ❌ Actual Result

```http
Status Code: 204 No Content
```

**Status:** ✅ PASS

---

# 🔟 DELETE /applications/{id} — Invalid Application ID

## 📌 Description

Verify API behavior when deleting an application using an invalid UUID.

## 🌐 Request

```http
DELETE /api/applications/12346abc
```

## ✅ Expected Result

The API should reject the invalid ID with a client error.

## ❌ Actual Result

```json
Status Code: 500 Internal Server Error

{
  "success": false,
  "message": "invalid input syntax for type uuid: \"12346abc\""
}
```

**Status:** ❌ FAIL

---

# 1️⃣1️⃣ PATCH /applications/{id}/status — Update Status

## 📌 Description

Verify that an application's status can be updated.

## 🌐 Request

```http
PATCH /api/applications/{id}/status
```

### Body

```json
{
  "status": "DRAFT"
}
```

## ✅ Expected Result

The application status should be updated successfully.

## ❌ Actual Result

```json
Status Code: 200 OK

{
  "status": "DRAFT"
}
```

**Status:** ✅ PASS

---

# 1️⃣2️⃣ PATCH /applications/{id}/status — Empty Status

## 📌 Description

Verify validation when an empty status value is submitted.

## 🌐 Request

```http
PATCH /api/applications/{id}/status
```

### Body

```json
{
  "status": " "
}
```

## ✅ Expected Result

The API should reject the request with a validation error.

## ❌ Actual Result

```json
Status Code: 404 Not Found

{
  "success": false,
  "message": "Application not found"
}
```

**Status:** ❌ FAIL

---

# 1️⃣3️⃣ PATCH /applications/{id}/passport — Update Passport Information

## 📌 Description

Verify that passport information can be updated successfully.

## 🌐 Request

```http
PATCH /api/applications/{id}/passport
```

## ✅ Expected Result

Passport information should be updated successfully.

## ❌ Actual Result

```json
Status Code: 200 OK
```

Passport information was updated successfully.

**Status:** ✅ PASS

---

# 1️⃣4️⃣ PATCH /applications/{id}/passport — Without Bearer Token

## 📌 Description

Verify authorization when updating passport information without authentication.

## 🌐 Request

```http
PATCH /api/applications/{id}/passport
```

## ✅ Expected Result

The API should return **401 Unauthorized**.

## ❌ Actual Result

```json
Status Code: 401 Unauthorized

{
  "success": false,
  "message": "Unauthorized"
}
```

**Status:** ✅ PASS

---

# 1️⃣5️⃣ GET /applications/{id}/pdf — Download PDF

## 📌 Description

Verify that the generated PDF can be downloaded.

## 🌐 Request

```http
GET /api/applications/{id}/pdf
```

## ✅ Expected Result

The PDF file should be downloaded successfully.

## ❌ Actual Result

```http
Status Code: 200 OK

File downloaded successfully.
```

**Status:** ✅ PASS

---

# 1️⃣6️⃣ GET /applications/{id}/pdf — Invalid ID Format

## 📌 Description

Verify API behavior when the application ID contains invalid characters.

## 🌐 Request

```http
GET /api/applications/{invalid_id}/pdf
```

## ✅ Expected Result

The API should reject the request with an error.

## ❌ Actual Result

```json
Status Code: 500 Internal Server Error

{
  "success": false,
  "message": "Application not found"
}
```

**Status:** ❌ FAIL

---

# 1️⃣7️⃣ POST /ocr/passport — Passport OCR

## 📌 Description

Verify OCR processing using a valid passport image.

## 🌐 Request

```http
POST /api/ocr/passport
```

## ✅ Expected Result

Passport data should be extracted successfully.

## ❌ Actual Result

```diff
- Status Code: 500 Internal Server Error
-
- Failed to process image
-
- Your credit balance is too low to access the Anthropic API.
```

**Status:** ❌ FAIL

---

# 1️⃣8️⃣ POST /ocr/passport — Empty Image

## 📌 Description

Verify validation when no image is uploaded.

## 🌐 Request

```http
POST /api/ocr/passport
```

### Body

```text
image → Empty
```

## ✅ Expected Result

The API should return a validation error.

## ❌ Actual Result

```json
Status Code: 400 Bad Request

{
  "error": "No image file provided"
}
```

**Status:** ✅ PASS

---

# 1️⃣9️⃣ GET /health — Health Check

## 📌 Description

Verify that the API health endpoint is operational.

## 🌐 Request

```http
GET /api/health
```

## ✅ Expected Result

The API should return **200 OK**.

## ❌ Actual Result

```json
Status Code: 200 OK

{
  "ok": true,
  "service": "smplifai-backend"
}
```

**Status:** ✅ PASS

---

# 2️⃣0️⃣ GET /health — Invalid Health Endpoint

## 📌 Description

Verify API behavior when an incorrect health endpoint is requested.

## 🌐 Request

```http
GET /api/he
```

## ✅ Expected Result

The API should return **404 Not Found**.

## ❌ Actual Result

```json
Status Code: 404 Not Found

{
  "success": false,
  "message": "Route not found",
  "path": "/api/he"
}
```

**Status:** ✅ PASS
