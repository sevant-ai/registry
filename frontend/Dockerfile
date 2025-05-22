# Build stage
FROM --platform=$BUILDPLATFORM node:20-alpine AS builder

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install --ignore-scripts

# Copy source code
COPY . .

# Build the Next.js app
RUN NEXTJS_IGNORE_ESLINT=1 npm run build

# Production stage
FROM --platform=$TARGETPLATFORM node:20-alpine

WORKDIR /app

# Install curl for health checks
RUN apk add --no-cache curl

# Copy package files
COPY package*.json ./

# Install production dependencies only
RUN npm install --only=production --ignore-scripts && \
    npm cache clean --force

# Copy built application
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/public ./public
COPY --from=builder /app/package.json ./package.json

# Expose port
EXPOSE 3000

# Start the application
CMD ["npm", "start"]

# Add this line to update system packages
RUN apk update && apk upgrade 