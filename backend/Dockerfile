# Build stage
FROM --platform=$BUILDPLATFORM node:18-alpine AS builder

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install --legacy-peer-deps --ignore-scripts

# Copy source code
COPY . .

# Build the application
RUN npm run build

# Production stage
FROM --platform=$TARGETPLATFORM node:18-alpine

WORKDIR /app

# Install curl for health checks
RUN apk add --no-cache curl

# Copy package files
COPY package*.json ./

# Install production dependencies only
RUN npm install --only=production --legacy-peer-deps --ignore-scripts && \
    npm cache clean --force

# Copy built application
COPY --from=builder /app/dist ./dist

# Expose port
EXPOSE 3001

# Start the application
CMD ["npm", "run", "start:prod"] 