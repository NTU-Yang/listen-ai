# Build stage
FROM golang:1.24-alpine AS builder

# Set the working directory
WORKDIR /app

# Copy go.mod and go.sum files and Download dependencies
COPY go.mod go.sum ./
RUN go mod download

# Copy the rest of the application code
COPY . .

# Build the application
RUN CGO_ENABLED=0 go build -o stat-service .

# Final stage
FROM alpine:latest

# Install sqlite for debugging
RUN apk add --no-cache sqlite-libs

# Set the working directory
WORKDIR /app

# Copy the binary from the builder stage
COPY --from=builder /app/stat-service .

# Create a directory for the database
RUN mkdir -p /data

# Expose the stat port
EXPOSE 8002

# Set default environment variables
ENV SQLITE_PATH=/data/listenai.db

# Define the command to run the app
CMD ["./stat-service"]
