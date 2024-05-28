# Stage 1: Build the Next.js application
FROM node:22-alpine AS builder

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the Next.js application
RUN npm run build

# Stage 2: Create the production image
FROM node:22-alpine AS production

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install only production dependencies
RUN npm install --only=production

# Copy the built Next.js application from the builder stage
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/public ./public
#COPY --from=builder /app/next.config.js ./
COPY --from=builder /app/package.json ./

# Expose the port the app runs on
EXPOSE 3000

# Set the command to start the application
CMD ["npm", "start"]
