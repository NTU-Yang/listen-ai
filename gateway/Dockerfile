# Use Node.js 20 slim image as the base
FROM node:20-slim

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install production dependencies
RUN npm install --omit=dev

# Copy the rest of the application code
COPY . .

# Expose the gateway port
EXPOSE 8000

# Command to run the service
CMD ["npm", "start"]
