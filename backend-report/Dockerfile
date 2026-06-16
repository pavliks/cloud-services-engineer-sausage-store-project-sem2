FROM golang:1.20-alpine AS builder

WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download

COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o backend-report .

FROM alpine:3.20

RUN addgroup -S app && adduser -S -G app app && apk add --no-cache ca-certificates
WORKDIR /app
COPY --from=builder /app/backend-report ./backend-report

EXPOSE 8080
USER app
CMD ["/app/backend-report"]
