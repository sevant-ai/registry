
# Sevant Registry Docker Setup

This repository contains the Docker configuration for the Sevant Registry application, including both frontend and backend services.

## Prerequisites

- Docker
- Docker Compose
- Git

## Environment Variables

Create a `.env` file in the root directory with the following variables:

```env
MONGODB_URI=your_mongodb_connection_string
SWAGGER_API_BASE_URL=your_swagger_api_base_url
SENDGRID_API_KEY=(Starts with SG)
JWT_SECRET=secretKey
JWT_EXPIRATION=24h
EMAIL_FROM=(Email)
SWAGGER_API_BASE_URL=https://api.swaggerhub.com/
FORGET_PASSWORD_BASE_URL_SERVER=your_password_reset_url_here
```

## Getting Started

1. Clone this repository:
   ```bash
   git clone <repository-url>
   cd registry
   ```

2. Create the `.env` file with your configuration

3. Build and start the containers:
   ```bash
   docker-compose up --build
   ```

The services will be available at:
- Frontend: http://localhost:3000
- Backend: http://localhost:3001

## Services

### Frontend
- Next.js application
- Runs on port 3000
- Depends on backend service

### Backend
- Node.js application
- Runs on port 3001
- Includes health checks
- Requires MongoDB connection

## Health Checks

Both services include health checks that run every 30 seconds to ensure the applications are running properly.

## Network

The services are connected through a bridge network named `app-network`.

# Sevant Service Registry
Sevant service registry dynamically depicts endpoints and their associated API's. (Domain Driven Context Language) provides a new language construct, by using a simple dot notation DDCL allows relationships to be formed between products, solutions and capabilities.

[DDCL] (https://analyticsavant.medium.com/domain-driven-context-language-899b099cd8d6)
>>>>>>> 83276a5530430cf9b11ebc4ddc1e6df42d9c5851
