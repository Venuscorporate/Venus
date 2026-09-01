# Deployment Guide

## Overview

This guide covers deploying Venus to various platforms including Vercel, Heroku, AWS, and Docker.

## Frontend Deployment (Vercel)

### Automatic Deployment

1. **Connect Repository to Vercel**
   - Go to [vercel.com](https://vercel.com)
   - Import GitHub repository
   - Select `frontend` as root directory
   - Add environment variables
   - Deploy

2. **Environment Variables**
   ```
   NEXT_PUBLIC_API_URL=https://api.youromain.com
   NEXT_PUBLIC_STRIPE_KEY=pk_live_...
   NEXT_PUBLIC_APP_NAME=Venus
   ```

### Manual Deployment

```bash
# Build the project
cd frontend
npm run build

# Deploy
vercel deploy --prod
```

## Backend Deployment (Heroku)

### Prerequisites
- Heroku CLI installed
- Heroku account
- PostgreSQL database

### Deploy Steps

```bash
# Login to Heroku
heroku login

# Create new app
heroku create venus-api

# Add environment variables
heroku config:set NODE_ENV=production
heroku config:set DATABASE_URL=postgresql://...
heroku config:set STRIPE_SECRET_KEY=sk_live_...

# Add PostgreSQL addon
heroku addons:create heroku-postgresql:standard-0

# Deploy
git push heroku main

# Run migrations
heroku run npm run migrate

# View logs
heroku logs --tail
```

## Admin Panel Deployment (Vercel)

```bash
cd admin
npm run build
vercel deploy --prod
```

## Docker Deployment

### Build Images

```bash
# Build frontend
docker build -t venus-frontend ./frontend

# Build backend
docker build -t venus-backend ./backend

# Build admin
docker build -t venus-admin ./admin
```

### Docker Compose

```bash
# Start all services
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down
```

## AWS Deployment

### Using ECS (Elastic Container Service)

1. **Create ECR Repositories**
   ```bash
   aws ecr create-repository --repository-name venus-frontend
   aws ecr create-repository --repository-name venus-backend
   ```

2. **Push Images**
   ```bash
   docker tag venus-frontend:latest <account>.dkr.ecr.<region>.amazonaws.com/venus-frontend:latest
   docker push <account>.dkr.ecr.<region>.amazonaws.com/venus-frontend:latest
   ```

3. **Create ECS Cluster and Services**
   - Use AWS Console or CloudFormation
   - Configure ALB (Application Load Balancer)
   - Set auto-scaling policies

### Using Elastic Beanstalk

```bash
# Install EB CLI
pip install awsebcli

# Initialize
eb init -p node.js-18 venus-app

# Create environment
eb create venus-env

# Set environment variables
eb setenv DATABASE_URL=... STRIPE_SECRET_KEY=...

# Deploy
eb deploy
```

## Database Setup

### PostgreSQL (AWS RDS)

```bash
# Create RDS Instance
aws rds create-db-instance \
  --db-instance-identifier venus-db \
  --db-instance-class db.t3.micro \
  --engine postgres \
  --master-username postgres \
  --master-user-password <password>

# Run migrations
npm run migrate
```

### MongoDB (MongoDB Atlas)

1. Create cluster at [mongodb.com/cloud](https://www.mongodb.com/cloud)
2. Get connection string
3. Add to environment variables:
   ```
   MONGODB_URI=mongodb+srv://user:password@cluster.mongodb.net/venus
   ```

## CDN Setup (Cloudflare)

1. Add domain to Cloudflare
2. Update nameservers at registrar
3. Create DNS records:
   ```
   app.venuscorporate.com -> Vercel (CNAME)
   api.venuscorporate.com -> Heroku/AWS (CNAME)
   admin.venuscorporate.com -> Vercel (CNAME)
   ```
4. Enable caching rules
5. Set up SSL/TLS

## SSL/TLS Certificates

### Let's Encrypt (Free)

```bash
# Using Certbot
certbot certonly --standalone -d venuscorporate.com -d *.venuscorporate.com
```

### AWS Certificate Manager (Free)

1. Go to ACM Console
2. Request certificate
3. Validate domain
4. Attach to ALB/CloudFront

## Monitoring & Logging

### Sentry (Error Tracking)

```bash
# Add Sentry
npm install @sentry/node @sentry/tracing
```

Add to backend:
```javascript
const Sentry = require('@sentry/node');
Sentry.init({ dsn: process.env.SENTRY_DSN });
```

### CloudWatch (AWS Logging)

```bash
# Install agent
npm install aws-xray-sdk
```

### ELK Stack (Elasticsearch, Logstash, Kibana)

```yaml
# docker-compose.yml addition
elasticsearch:
  image: docker.elastic.co/elasticsearch/elasticsearch:8.0.0
  
kibana:
  image: docker.elastic.co/kibana/kibana:8.0.0
```

## Performance Optimization

### Caching Strategy

```bash
# Redis
REDIS_URL=redis://cache.example.com:6379

# CloudFront
CloudFront distribution for static assets
```

### Database Optimization

```sql
-- Create indexes
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_documents_user_id ON documents(user_id);
CREATE INDEX idx_payments_status ON payments(status);
```

## Backup Strategy

### Database Backup

```bash
# PostgreSQL
pg_dump venus_db > backup.sql

# Restore
psql venus_db < backup.sql
```

### Automated Backups

- AWS RDS: Enable automatic backups (7+ days)
- MongoDB Atlas: Enable backup snapshots
- S3: Enable versioning for uploads

## Health Checks

### Endpoint Monitoring

```bash
# Health check endpoint
GET /api/health

Response:
{
  "status": "healthy",
  "database": "connected",
  "cache": "connected",
  "timestamp": "2026-09-01T13:00:00Z"
}
```

### Uptime Monitoring

- Use services like UptimeRobot
- Configure alerts for downtime
- Set up automated incident reporting

## Rollback Procedure

### Vercel
```bash
vercel rollback
```

### Heroku
```bash
heroku releases
heroku rollback v42
```

### Docker
```bash
# Revert to previous image
docker-compose down
git checkout previous-commit
docker-compose up -d
```

## Post-Deployment Checklist

- [ ] All services running and healthy
- [ ] Database migrations successful
- [ ] API endpoints responding
- [ ] Frontend loading correctly
- [ ] Admin panel accessible
- [ ] Payments processing
- [ ] OCR service operational
- [ ] Email notifications working
- [ ] Error logging operational
- [ ] Monitoring/alerts configured
- [ ] SSL certificates valid
- [ ] Backups running
- [ ] Load testing completed
- [ ] Security scan passed
- [ ] Performance baseline met

---

For questions or issues, open a GitHub issue or contact support@venuscorporate.com