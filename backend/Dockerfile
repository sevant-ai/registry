# Build stage
FROM --platform=$BUILDPLATFORM node:18-alpine AS builder

WORKDIR /app

# Install build dependencies
RUN apk add --no-cache python3 make g++

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install --legacy-peer-deps --ignore-scripts && \
    npm rebuild bcrypt --build-from-source

# Copy source code
COPY . .

# Build the application
RUN npm run build

# Production stage
FROM --platform=$TARGETPLATFORM node:18-alpine

WORKDIR /app

# Install curl for health checks and build dependencies for bcrypt
RUN apk add --no-cache curl python3 make g++

# Copy package files
COPY package*.json ./

# Install production dependencies only and rebuild bcrypt
RUN npm install --only=production --legacy-peer-deps --ignore-scripts && \
    npm rebuild bcrypt --build-from-source && \
    npm cache clean --force

# Copy built application
COPY --from=builder /app/dist ./dist

# Expose port
EXPOSE 3001

# Start the application
CMD ["npm", "run", "start:prod"] 