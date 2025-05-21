# Use official Node.js LTS image
FROM node:20-alpine

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json (or yarn.lock) first for better caching
COPY package.json ./
# If you use npm:
RUN npm install
# If you use yarn, replace above with:
# RUN yarn install

# Copy the rest of your application code
COPY . .

# Build the Next.js app
RUN NEXTJS_IGNORE_ESLINT=1 npm run build

# Expose the port Next.js will run on
EXPOSE 3000

# Start the Next.js app
CMD ["npm", "start"]

# Add this line to update system packages
RUN apk update && apk upgrade 