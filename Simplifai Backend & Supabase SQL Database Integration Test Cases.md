# Simplifai Backend API Test Cases Report

---

## 1. GET /applications — Müraciət siyahısı (login with bearer token)

### Request
```http
GET https://smplifai-backend.vercel.app/api/applications
```

### Actual Result
```json
Status code: 200 OK

[
  {
    "id": "ead61859-f979-4283-9f95-4a50409216b1",
    "user_id": "a3c38e71-9784-4b8c-81af-9692a2aa8373",
    "type": "Enrollment Agreement",
    "email": "leman.qrb@gmail.com",
    "phone": "+4488866625",
    "passport_data": {},
    "file_url": "https://tcrdbtaksnqezkbzgfys.supabase.co/storage/v1/object/public/passports/a3c38e71-9784-4b8c-81af-9692a2aa8373-1779897441566.pdf",
    "status": "documents_uploaded",
    "created_at": "2026-05-27T15:57:21.96399+00:00",
    "updated_at": "2026-05-27T15:57:21.96399+00:00",
    "documents_uploaded": true,
    "filled_form_url": null
  }
]
```

### Database Check
```sql
Select * from applications where id='ead61859-f979-4283-9f95-4a50409216b1';
```

---

## 2. GET /applications — Bearer tokensiz yoxlanış

### Request
```http
GET https://smplifai-backend.vercel.app/api/applications
```

### Actual Result
```json
Status code: 401 Unauthorized

{
  "success": false,
  "message": "Unauthorized"
}
```

---

## 3. POST /applications — Yeni application yaratmaq

### Request
```http
POST https://smplifai-backend.vercel.app/api/applications
```

### Body
```json
{
  "type": "My application"
}
```

### Actual Result
```json
Status code: 201 Created

{
  "id": "ef7a2867-3c5d-4475-aea9-aceb7681ef5d",
  "user_id": "a3c38e71-9784-4b8c-81af-9692a2aa8373",
  "type": "My application",
  "email": null,
  "phone": null,
  "passport_data": null,
  "file_url": null,
  "status": "DRAFT",
  "created_at": "2026-05-15T15:24:51.323321+00:00",
  "updated_at": "2026-05-15T15:24:51.323321+00:00"
}
```

### Database Check
```sql
Select * from applications where id='ef7a2867-3c5d-4475-aea9-aceb7681ef5d';
```

---

## 4. POST /applications — Endpoint natamam yazılaraq yoxlanış

### Request
```http
POST https://smplifai-backend.vercel.app/api/applicatio
```

### Body
```json
{
  "type": "Tests"
}
```

### Actual Result
```json
Status code: 404 Not Found

{
  "success": false,
  "message": "Route not found",
  "path": "/api/applicatio"
}
```

---

## 5. POST /applications/submit — Tam müraciət göndərmək

### Request
```http
POST https://smplifai-backend.vercel.app/api/applications/submit
```

### Actual Result
```json
Status code: 201 Created

{
  "id": "bcc1edb0-a934-4d35-931f-24799f5ef29c",
  "user_id": "a3c38e71-9784-4b8c-81af-9692a2aa8373",
  "type": "My Passport",
  "email": "lexi@example.com",
  "phone": "+994501234567",
  "passport_data": {
    "surname": "Doe",
    "firstName": "Lexi"
  },
  "file_url": "https://tcrdbtaksnqezkbzgfys.supabase.co/storage/v1/object/public/passports/a3c38e71-9784-4b8c-81af-9692a2aa8373-1778942992023.pdf",
  "status": "pending",
  "created_at": "2026-05-16T14:49:52.813016+00:00",
  "updated_at": "2026-05-16T14:49:52.813016+00:00"
}
```

---

## 6. POST /applications/submit — Bearer tokensiz yoxlanış

### Request
```http
POST https://smplifai-backend.vercel.app/api/applications/submit
```

### Actual Result
```json
Status code: 401 Unauthorized

{
  "success": false,
  "message": "Unauthorized"
}
```

---

## 7. GET /applications/{id} — Valid ID ilə tək müraciət

### Request
```http
GET https://smplifai-backend.vercel.app/api/applications/7162f485-07a7-4679-ba5b-58062b27e55a
```

### Actual Result
```json
Status code: 200 OK

{
  "id": "7162f485-07a7-4679-ba5b-58062b27e55a",
  "user_id": "a3c38e71-9784-4b8c-81af-9692a2aa8373",
  "type": "My Passport",
  "email": null,
  "phone": null,
  "passport_data": null,
  "file_url": null,
  "status": "DRAFT",
  "created_at": "2026-04-21T00:12:40.091239+00:00",
  "updated_at": "2026-04-21T00:12:40.091239+00:00"
}
```

---

## 8. GET /applications/{id} — Invalid ID ilə yoxlanış

### Request
```http
GET https://smplifai-backend.vercel.app/api/applications/7162f485-07a7-4679-ba5b-58062b27
```

### Actual Result
```json
Status code: 404 Not Found

{
  "success": false,
  "message": "Application not found"
}
```

---

## 9. DELETE /applications/{id} — Valid ID ilə müraciəti silmək

### Request
```http
DELETE https://smplifai-backend.vercel.app/api/applications/ec9cc86e-d6c7-4098-a84e-d177dd6727c7
```

### Actual Result
```json
Status code: 204 No Content
```

---

## 10. DELETE /applications/{id} — Invalid ID ilə müraciəti silmək

### Request
```http
DELETE https://smplifai-backend.vercel.app/api/applications/12346abc
```

### Actual Result
```json
Status code: 500 Internal Server Error

{
  "success": false,
  "message": "invalid input syntax for type uuid: \"12346abc\""
}
```

---

## 11. PATCH /applications/{id}/status — Status dəyişmək

### Request
```http
PATCH https://smplifai-backend.vercel.app/api/applications/bfd00da0-5df6-4783-87da-95b7006e1945/status
```

### Body
```json
{
  "status": "DRAFT"
}
```

### Actual Result
```json
Status code: 200 OK

{
  "id": "bfd00da0-5df6-4783-87da-95b7006e1945",
  "status": "DRAFT"
}
```

---

## 12. PATCH /applications/{id}/status — Status boş göndərərək yoxlama

### Request
```http
PATCH https://smplifai-backend.vercel.app/api/applications/616413fb-fd41-4ca6-9b9a-177ecd6534f9/status
```

### Body
```json
{
  "status": " "
}
```

### Actual Result
```json
Status code: 404 Not Found

{
  "success": false,
  "message": "Application not found"
}
```

---

## 13. PATCH /applications/{id}/passport — Passport məlumatlarını yeniləmək

### Request
```http
PATCH https://smplifai-backend.vercel.app/api/applications/bfd00da0-5df6-4783-87da-95b7006e1945/passport
```

### Body
```json
{
  "passport_data": {
    "firstName": "Dakota",
    "surname": "Doe",
    "passportNo": "A1234567",
    "dateOfIssue": "2020-01-01",
    "sex": "M",
    "nationality": "ENG",
    "dateOfExpiry": "2030-01-01",
    "dateOfBirth": "1990-01-01",
    "code": "AZE",
    "personalNo": "1ZV234A"
  }
}
```

### Actual Result
```json
Status code: 200 OK

{
  "passport_data": {
    "sex": "M",
    "code": "AZE",
    "surname": "Doe",
    "firstName": "Dakota",
    "passportNo": "A1234567",
    "personalNo": "1ZV234A",
    "dateOfBirth": "1990-01-01",
    "dateOfIssue": "2020-01-01",
    "nationality": "ENG",
    "dateOfExpiry": "2030-01-01"
  }
}
```

---

## 14. PATCH /applications/{id}/passport — Bearer tokensiz yoxlanış

### Request
```http
PATCH https://smplifai-backend.vercel.app/api/applications/bfd00da0-5df6-4783-87da-95b7006e1945/passport
```

### Actual Result
```json
Status code: 401 Unauthorized

{
  "success": false,
  "message": "Unauthorized"
}
```

---

## 15. GET /applications/{id}/pdf — PDF yükləmək

### Request
```http
GET https://smplifai-backend.vercel.app/api/applications/ef7a2867-3c5d-4475-aea9-aceb7681ef5d/pdf
```

### Actual Result
```json
Status code: 200 OK

Download file
```

---

## 16. GET /applications/{id}/pdf — ID daxilində boşluq ilə yoxlama

### Request
```http
GET https://smplifai-backend.vercel.app/api/applications/ef7a2867-3c5d-4475-aea9-aceb7681ef%205d/pdf
```

### Actual Result
```json
Status code: 500 Internal Server Error

{
  "success": false,
  "message": "Application not found"
}
```

---

## 17. POST /ocr/passport — Passport OCR yoxlanışı

### Request
```http
POST https://smplifai-backend.vercel.app/api/ocr/passport
```

### Actual Result

```diff
- Status code: 500 Failed to process image
-
- {
-   "error": "Failed to process image",
-   "details": "Your credit balance is too low to access the Anthropic API."
- }
```

---

## 18. POST /ocr/passport — Empty image ilə yoxlanış

### Request
```http
POST https://smplifai-backend.vercel.app/api/ocr/passport
```

### Body
```text
image → Send empty value
```

### Actual Result
```json
Status code: 400 Bad Request

{
  "error": "No image file provided"
}
```

---

## 19. GET /health — Server health check

### Request
```http
GET https://smplifai-backend.vercel.app/api/health
```

### Actual Result
```json
Status code: 200 OK

{
  "ok": true,
  "service": "smplifai-backend"
}
```

---

## 20. GET /health — Endpoint natamam yazılaraq yoxlanış

### Request
```http
GET https://smplifai-backend.vercel.app/api/he
```

### Actual Result
```json
Status code: 404 Not Found

{
  "success": false,
  "message": "Route not found",
  "path": "/api/he"
}
```
