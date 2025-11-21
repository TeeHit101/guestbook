FROM golang:1.24-alpine AS builder
WORKDIR /app

COPY go.mod go.sum ./
RUN go mod tidy
RUN go mod download

COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o backend .


FROM alpine:3.19

RUN apk update && apk add --no-cache curl

RUN apk add --no-cache ca-certificates

WORKDIR /app


COPY --from=builder /app/backend /app/backend


RUN chown -R 1001:0 /app && chmod -R g+rwX /app

USER 1001

EXPOSE 8080
ENTRYPOINT ["/app/backend"]
