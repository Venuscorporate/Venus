# README.md
A full-stack service application with integrated frontend, backend, and storage solutions.

**Live Demo**: [venus-corporate-service-fixed.vercel.app](https://venus-corporate-service-fixed.vercel.app)

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Development](#development)
- [Testing](#testing)
- [Deployment](#deployment)
- [Environment Variables](#environment-variables)
- [API Documentation](#api-documentation)
- [Admin Panel](#admin-panel)
- [Troubleshooting](#troubleshooting)

---

## 🎯 Project Overview

Venus is a modern, scalable service designed to provide seamless integration between:
- **Frontend**: Responsive web interface with OCR document scanning
- **Backend**: RESTful API server with payment gateway integration
- **Storage**: Database and file management
- **Admin Panel**: Dashboard for managing users, transactions, and documents
- **Deployment**: Cloud-ready architecture

This repository contains all components needed for local development and testing.

---

## 🛠 Tech Stack

### Frontend
- **Framework**: Next.js / React
- **Styling**: Tailwind CSS / CSS Modules
- **State Management**: Redux / Context API
- **OCR**: Tesseract.js / AWS Textract
- **Testing**: Jest, React Testing Library, Cypress
- **Build Tool**: Webpack / Vite

### Backend
- **Runtime**: Node.js / Python
- **Framework**: Express.js / FastAPI
- **Database**: PostgreSQL / MongoDB
- **ORM**: Prisma / SQLAlchemy
- **Payment Gateway**: Stripe / PayPal / Square
- **OCR Service**: Tesseract / AWS Textract / Google Vision
- **Testing**: Jest / Pytest
- **API Documentation**: Swagger / OpenAPI

### Admin Panel
- **Framework**: React / Next.js with Admin Dashboard
- **Charts**: Chart.js / Recharts
- **Tables**: React Table / AG Grid
- **Authentication**: JWT / OAuth

### Storage & Infrastructure
- **Database**: PostgreSQL / MongoDB
- **File Storage**: AWS S3 / Azure Blob Storage / Local Storage
- **Cache**: Redis
- **Deployment**: Vercel (Frontend) / Heroku / AWS / Docker

---

## 📁 Project Structure

```
Venus/
├── frontend/                    # Next.js/React application
│   ├── public/                 # Static assets
│   ├── src/
│   │   ├── pages/             # Page components
│   │   ├── components/        # Reusable components
│   │   │   ├── ocr/          # OCR document scanner
│   │   │   └── payment/      # Payment gateway components
│   │   ├── hooks/             # Custom React hooks
│   │   ├── utils/             # Utility functions
│   │   ├── styles/            # Global styles
│   │   └── tests/             # Jest tests
│   ├── package.json
│   ├── .env.example
│   └── next.config.js
│
├── backend/                     # Express.js/Node server
│   ├── src/
│   │   ├── routes/
│   │   │   ├── auth.js        # Authentication
│   │   │   ├── users.js       # User management
│   │   │   ├── documents.js   # Document upload/OCR
│   │   │   ├── payment.js     # Payment processing
│   │   │   ├── ocr.js         # OCR API
│   │   │   └── admin.js       # Admin panel APIs
│   │   ├── controllers/        # Business logic
│   │   ├── models/             # Database models
│   │   ├── middleware/         # Express middleware
│   │   ├── services/
│   │   │   ├── ocr.js         # OCR service
│   │   │   ├── payment.js     # Payment service
│   │   │   └── email.js       # Email service
│   │   ├── utils/
│   │   │   └── validators.js  # Input validation
│   │   ├── config/
│   │   │   ├── database.js
│   │   │   ├── payment.js     # Payment gateway config
│   │   │   └── ocr.js         # OCR service config
│   │   └── tests/
│   ├── package.json
│   ├── .env.example
│   └── server.js
│
├── admin/                       # Admin dashboard
│   ├── src/
│   │   ├── pages/
│   │   │   ├── dashboard.tsx  # Main dashboard
│   │   │   ├── users/         # User management
│   │   │   ├── documents/     # Document management
│   │   │   ├── payments/      # Payment tracking
│   │   │   ├── ocr/           # OCR history
│   │   │   ├── reports/       # Analytics & reports
│   │   │   └── settings/      # Admin settings
│   │   ├── components/
│   │   ├── hooks/
│   │   └── styles/
│   ├── package.json
│   └── .env.example
│
├── .github/
│   └── workflows/
│       ├── test.yml           # CI/CD tests
│       └── deploy.yml         # Deployment
│
├── docker-compose.yml         # Docker services
├── .env.example
├── .gitignore
└── README.md
```

---

## 📦 Prerequisites

- **Node.js** v18+
- **npm** v9+ or **yarn** v3+
- **Git**
- **Docker** & **Docker Compose** (optional)
- **PostgreSQL** v13+ or **MongoDB** v5+

---

## 🚀 Getting Started

### 1. Clone Repository

```bash
git clone https://github.com/Venuscorporate/Venus.git
cd Venus
```

### 2. Install Dependencies

```bash
# Frontend
cd frontend && npm install

# Backend
cd ../backend && npm install

# Admin Dashboard
cd ../admin && npm install
```

### 3. Set Up Environment Variables

```bash
# Copy templates
cp .env.example .env

# Frontend
cd frontend && cp .env.example .env.local

# Backend
cd ../backend && cp .env.example .env

# Admin
cd ../admin && cp .env.example .env.local
```

### 4. Start Services (Docker)

```bash
docker-compose up -d
```

### 5. Run Database Migrations

```bash
cd backend
npm run migrate
npm run seed
```

---

## 💻 Development

### Start All Services

**Terminal 1 - Frontend:**
```bash
cd frontend
npm run dev
# http://localhost:3000
```

**Terminal 2 - Backend:**
```bash
cd backend
npm run dev
# http://localhost:5000
# API Docs: http://localhost:5000/api-docs
```

**Terminal 3 - Admin Panel:**
```bash
cd admin
npm run dev
# http://localhost:3001
```

---

## 🧪 Testing

### Frontend Tests
```bash
cd frontend
npm test
npm run test:coverage
```

### Backend Tests
```bash
cd backend
npm test
npm run test:coverage
```

### E2E Tests
```bash
cd frontend
npm run cypress:run
```

### Full Test Suite
```bash
npm run test:all
```

---

## 🔐 Environment Variables

### Backend (.env)

```
NODE_ENV=development
PORT=5000
DATABASE_URL=postgresql://venus_user:venus_password@localhost:5432/venus_db
REDIS_URL=redis://localhost:6379
JWT_SECRET=your_jwt_secret_key

# OCR Service
OCR_SERVICE=tesseract  # Options: tesseract, aws-textract, google-vision
OCR_API_KEY=your_ocr_api_key
OCR_ENDPOINT=https://api.ocr-service.com

# Payment Gateway
PAYMENT_PROVIDER=stripe  # Options: stripe, paypal, square
STRIPE_SECRET_KEY=sk_test_...
STRIPE_PUBLISHABLE_KEY=pk_test_...
STRIPE_WEBHOOK_SECRET=whsec_...

# PayPal (Alternative)
PAYPAL_CLIENT_ID=your_paypal_client_id
PAYPAL_CLIENT_SECRET=your_paypal_secret
PAYPAL_MODE=sandbox

# Square (Alternative)
SQUARE_ACCESS_TOKEN=sq_test_...
SQUARE_LOCATION_ID=your_location_id

# AWS (for S3 & Textract)
AWS_REGION=us-east-1
AWS_ACCESS_KEY_ID=your_aws_key
AWS_SECRET_ACCESS_KEY=your_aws_secret
AWS_S3_BUCKET=venus-uploads

# Admin Panel
ADMIN_JWT_SECRET=admin_secret_key
ADMIN_EMAIL_DOMAIN=@venuscorporate.com
```

### Frontend (.env.local)

```
NEXT_PUBLIC_API_URL=http://localhost:5000
NEXT_PUBLIC_APP_NAME=Venus
NEXT_PUBLIC_STRIPE_KEY=pk_test_...
NEXT_PUBLIC_OCR_ENABLED=true
```

---

## 📚 API Documentation

### API Endpoints

**Health Check:**
```
GET /api/health
```

**Authentication:**
```
POST   /api/auth/register
POST   /api/auth/login
POST   /api/auth/logout
POST   /api/auth/refresh
```

**Users:**
```
GET    /api/users
POST   /api/users
GET    /api/users/:id
PUT    /api/users/:id
DELETE /api/users/:id
GET    /api/users/:id/documents
```

**Document Upload & OCR:**
```
POST   /api/documents/upload        # Upload document
GET    /api/documents/:id           # Get document details
GET    /api/documents/:id/ocr       # Get OCR results
POST   /api/documents/:id/process   # Process with OCR
DELETE /api/documents/:id
GET    /api/documents/user/:userId  # Get user documents
```

**OCR Service:**
```
POST   /api/ocr/process             # Process document
POST   /api/ocr/batch               # Batch processing
GET    /api/ocr/history             # OCR history
GET    /api/ocr/results/:jobId
```

**Payments:**
```
POST   /api/payments/create         # Create payment
GET    /api/payments/:id            # Get payment details
POST   /api/payments/:id/confirm    # Confirm payment
GET    /api/payments/user/:userId   # User payments
POST   /api/payments/webhook        # Payment webhook
GET    /api/payments/invoice/:id    # Download invoice
```

**Admin APIs:**
```
GET    /api/admin/dashboard         # Dashboard stats
GET    /api/admin/users             # All users
GET    /api/admin/documents         # All documents
GET    /api/admin/payments          # All payments
GET    /api/admin/analytics         # Analytics data
POST   /api/admin/settings/update   # Update settings
GET    /api/admin/logs              # Activity logs
POST   /api/admin/users/:id/suspend # Suspend user
```

---

## 🎛️ Admin Panel Features

### Dashboard
- Real-time statistics (users, documents, payments)
- Revenue charts and graphs
- Recent activity feed
- System health monitoring

### User Management
- View all users
- Edit user details
- Suspend/activate users
- View user documents and payments
- Export user data

### Document Management
- View all uploaded documents
- OCR status and results
- Verify document authenticity
- Download/export documents
- Batch operations

### Payment Management
- View all transactions
- Payment status tracking
- Refund processing
- Invoice generation
- Payment reconciliation

### OCR Management
- OCR processing history
- Retry failed jobs
- View extracted data
- Quality metrics
- Service status

### Reports & Analytics
- Revenue reports
- User growth charts
- Document processing stats
- Payment gateway analytics
- Export reports

### Settings
- System configuration
- Payment gateway settings
- OCR service configuration
- Email templates
- Admin user management

---

## 🛠️ Integration Guides

### OCR Integration (Tesseract.js)

```javascript
// Backend service
const Tesseract = require('tesseract.js');

async function processDocument(imagePath) {
  const result = await Tesseract.recognize(imagePath);
  return result.data.text;
}
```

### Payment Gateway Integration (Stripe)

```javascript
// Backend
const stripe = require('stripe')(process.env.STRIPE_SECRET_KEY);

async function createPayment(amount, currency) {
  const intent = await stripe.paymentIntents.create({
    amount: amount * 100,
    currency: currency,
  });
  return intent;
}
```

### Payment Gateway Integration (PayPal)

```javascript
// Backend
const paypalClient = require('@paypal/checkout-server-sdk');

async function createOrder(amount) {
  const request = new paypalClient.orders.OrdersCreateRequest();
  request.prefer("return=representation");
  request.body = {
    intent: 'CAPTURE',
    purchase_units: [{amount: {currency_code: 'USD', value: amount}}]
  };
  return paypalClient.client().execute(request);
}
```

---

## 🌐 Deployment

### Frontend (Vercel)
```bash
cd frontend
npm run build
vercel deploy
```

### Backend (Heroku)
```bash
heroku login
heroku create venus-api
git push heroku main
heroku run npm run migrate
```

### Admin (Vercel)
```bash
cd admin
npm run build
vercel deploy
```

### Docker
```bash
docker build -t venus-frontend ./frontend
docker build -t venus-backend ./backend
docker build -t venus-admin ./admin
docker-compose -f docker-compose.prod.yml up
```

---

## 🐛 Troubleshooting

### Database Connection Error
```bash
# Check PostgreSQL
psql -U venus_user -d venus_db

# Reset database
npm run backend -- db:reset
```

### Payment Gateway Not Working
- Verify API keys in .env
- Check webhook configuration
- Test with sandbox credentials first

### OCR Service Issues
- Verify OCR_API_KEY and endpoint
- Check image quality and format
- Ensure sufficient API quota

### Admin Panel Access Denied
- Verify JWT_SECRET matches
- Check admin user permissions
- Clear browser cache and cookies

---

## 📋 Pre-Deployment Checklist

- [ ] All tests passing
- [ ] Environment variables configured
- [ ] Database migrations complete
- [ ] Payment gateway tested
- [ ] OCR service operational
- [ ] Admin panel accessible
- [ ] API documentation updated
- [ ] Security headers configured
- [ ] CORS properly set
- [ ] SSL/TLS certificates ready

---

## 📝 License

MIT License - See LICENSE file

---

## 📧 Support

- **GitHub Issues**: [Create an issue](https://github.com/Venuscorporate/Venus/issues)
- **Email**: support@venuscorporate.com

---

**Last Updated**: September 1, 2026  
**Status**: 🟢 Active Development
