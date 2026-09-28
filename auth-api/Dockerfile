FROM golang:1.18-alpine AS builder
WORKDIR /app
COPY . .
RUN go mod init github.com/bortizf/microservice-app-example/auth-api 2>/dev/null || true
RUN go mod tidy
RUN CGO_ENABLED=0 GOOS=linux go build -ldflags="-w -s" -o auth-api .

FROM alpine:3.18
WORKDIR /app
COPY --from=builder /app/auth-api .
ENV AUTH_API_PORT=8000
ENV USERS_API_ADDRESS=http://users-api:8083
ENV JWT_SECRET=PRFT
EXPOSE 8000
CMD ["./auth-api"]