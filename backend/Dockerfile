# Stage 1: Build the Go binary
FROM golang:1.20-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .
RUN go build -o main .

# Stage 2: Create a small image for running the Go binary
FROM scratch

WORKDIR /app
COPY --from=builder /etc/passwd /etc/group /etc/
COPY --from=builder /app/main /app/

# switch to non-root user
USER 1000:1000

EXPOSE 8080
ENTRYPOINT ["./main"]

