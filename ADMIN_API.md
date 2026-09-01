# Admin Panel API Routes Documentation

## Overview

The Venus Admin Panel provides comprehensive backend APIs for managing users, documents, payments, OCR processing, and system analytics.

---

## Authentication

All admin endpoints require JWT authentication in the `Authorization` header:

```
Authorization: Bearer <admin_jwt_token>
```

### Admin Login
```
POST /api/admin/auth/login
Content-Type: application/json

{
  "email": "admin@venuscorporate.com",
  "password": "your_password"
}

Response:
{
  "token": "eyJhbGc...",
  "user": {
    "id": "admin_id",
    "email": "admin@venuscorporate.com",
    "role": "superadmin",
    "permissions": ["all"]
  }
}
```

---

## Dashboard Endpoints

### Get Dashboard Overview
```
GET /api/admin/dashboard
Query Params: ?period=30d (7d, 30d, 90d, 1y)

Response:
{
  "stats": {
    "totalUsers": 1500,
    "activeUsers": 1200,
    "totalDocuments": 4500,
    "processedDocuments": 4200,
    "totalRevenue": 125000,
    "pendingPayments": 15000,
    "ocrProcessed": 4200,
    "ocrFailed": 45
  },
  "charts": {
    "revenueChart": [...],
    "userGrowth": [...],
    "documentProcessing": [...]
  },
  "recentActivity": [...],
  "systemHealth": {
    "databaseStatus": "healthy",
    "cacheStatus": "healthy",
    "paymentGateway": "connected",
    "ocrService": "operational"
  }
}
```

---

## User Management

### List All Users
```
GET /api/admin/users
Query Params:
  - page=1
  - limit=50
  - search=query
  - status=active|suspended|deleted
  - sortBy=createdAt|name|email
  - sortOrder=asc|desc

Response:
{
  "data": [
    {
      "id": "user_id",
      "email": "user@example.com",
      "name": "John Doe",
      "status": "active",
      "documentCount": 3,
      "totalSpent": 5000,
      "createdAt": "2026-01-15T10:30:00Z",
      "lastLogin": "2026-09-01T13:00:00Z"
    }
  ],
  "total": 1500,
  "page": 1,
  "pages": 30
}
```

### Get User Details
```
GET /api/admin/users/:userId

Response:
{
  "id": "user_id",
  "email": "user@example.com",
  "name": "John Doe",
  "phone": "+1234567890",
  "status": "active",
  "role": "customer",
  "documents": [...],
  "payments": [...],
  "subscriptionStatus": "active",
  "subscriptionEndDate": "2027-09-01",
  "createdAt": "2026-01-15T10:30:00Z",
  "lastLogin": "2026-09-01T13:00:00Z"
}
```

### Update User
```
PUT /api/admin/users/:userId
Content-Type: application/json

{
  "name": "Updated Name",
  "email": "newemail@example.com",
  "status": "active",
  "phone": "+1234567890"
}

Response: Updated user object
```

### Suspend User
```
POST /api/admin/users/:userId/suspend
Content-Type: application/json

{
  "reason": "Policy violation",
  "duration": "permanent"
}

Response:
{
  "success": true,
  "message": "User suspended",
  "userId": "user_id",
  "suspendedUntil": null
}
```

---

## Document Management

### List All Documents
```
GET /api/admin/documents
Query Params:
  - page=1
  - limit=50
  - status=pending|processing|verified|rejected
  - type=passport|license|visa|proof_of_residence
  - userId=user_id
  - ocrStatus=pending|completed|failed

Response:
{
  "data": [
    {
      "id": "doc_id",
      "userId": "user_id",
      "userName": "John Doe",
      "fileName": "passport.jpg",
      "documentType": "passport",
      "uploadedAt": "2026-08-20T10:30:00Z",
      "status": "verified",
      "ocrStatus": "completed",
      "fileSize": 2048000
    }
  ],
  "total": 4500,
  "stats": {
    "totalDocuments": 4500,
    "verified": 4200,
    "pending": 250,
    "rejected": 50
  }
}
```

### Verify Document
```
POST /api/admin/documents/:documentId/verify
Content-Type: application/json

{
  "status": "verified",
  "notes": "Verified successfully",
  "expiryDate": "2030-12-31"
}

Response:
{
  "success": true,
  "message": "Document verified",
  "documentId": "doc_id",
  "status": "verified"
}
```

### Reprocess OCR
```
POST /api/admin/documents/:documentId/reprocess-ocr
Content-Type: application/json

{
  "ocrService": "tesseract",
  "forceReprocess": true
}

Response:
{
  "success": true,
  "message": "OCR reprocessing started",
  "jobId": "job_id",
  "status": "processing"
}
```

---

## Payment Management

### List All Payments
```
GET /api/admin/payments
Query Params:
  - page=1
  - limit=50
  - status=pending|completed|failed|refunded
  - gateway=stripe|paypal|square
  - userId=user_id
  - dateFrom=2026-01-01
  - dateTo=2026-12-31

Response:
{
  "data": [
    {
      "id": "payment_id",
      "userId": "user_id",
      "userName": "John Doe",
      "amount": 1500,
      "currency": "USD",
      "status": "completed",
      "gateway": "stripe",
      "gatewayTransactionId": "ch_...",
      "createdAt": "2026-08-15T10:30:00Z",
      "completedAt": "2026-08-15T10:35:00Z"
    }
  ],
  "total": 2500,
  "totalAmount": 3750000,
  "stats": {
    "successRate": 98.5,
    "totalFailed": 38,
    "totalRefunded": 12
  }
}
```

### Process Refund
```
POST /api/admin/payments/:paymentId/refund
Content-Type: application/json

{
  "amount": 1500,
  "reason": "Customer request",
  "notes": "Requested refund"
}

Response:
{
  "success": true,
  "message": "Refund processed",
  "refundId": "ref_...",
  "amount": 1500,
  "status": "completed"
}
```

---

## OCR Management

### List OCR Jobs
```
GET /api/admin/ocr/jobs
Query Params:
  - page=1
  - limit=50
  - status=pending|processing|completed|failed

Response:
{
  "data": [
    {
      "id": "job_id",
      "documentId": "doc_id",
      "userId": "user_id",
      "status": "completed",
      "service": "tesseract",
      "confidence": 0.95,
      "processedAt": "2026-08-20T10:35:00Z",
      "processingTime": 5000
    }
  ],
  "total": 4200,
  "stats": {
    "successRate": 93.3,
    "averageProcessingTime": 4500,
    "totalProcessed": 4200,
    "totalFailed": 300
  }
}
```

### Retry Failed OCR
```
POST /api/admin/ocr/jobs/:jobId/retry
Content-Type: application/json

{
  "service": "tesseract",
  "forceReprocess": true
}

Response:
{
  "success": true,
  "message": "OCR job retry started",
  "newJobId": "new_job_id",
  "status": "processing"
}
```

---

## Reports & Analytics

### Get Revenue Report
```
GET /api/admin/reports/revenue
Query Params:
  - period=month|quarter|year
  - dateFrom=2026-01-01
  - dateTo=2026-12-31

Response:
{
  "period": "2026-08",
  "totalRevenue": 125000,
  "byGateway": {
    "stripe": 75000,
    "paypal": 35000,
    "square": 15000
  },
  "byService": {...},
  "chart": [...]
}
```

### Get User Growth Report
```
GET /api/admin/reports/users

Response:
{
  "totalUsers": 1500,
  "newUsers": 450,
  "activeUsers": 1200,
  "churnRate": 5.2,
  "chart": [...]
}
```

---

## Error Responses

All endpoints return errors in this format:

```json
{
  "success": false,
  "error": {
    "code": "UNAUTHORIZED",
    "message": "Invalid or expired token",
    "details": "Token expired at 2026-09-01T12:00:00Z"
  }
}
```

---

**For complete API documentation, see ADMIN_API.md**