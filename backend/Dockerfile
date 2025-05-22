# Development
FROM golang:1.23.0 AS development

RUN apt-get update && \
    apt-get install -y wget gnupg default-mysql-client && \
    echo "deb http://apt.postgresql.org/pub/repos/apt bookworm-pgdg main" > /etc/apt/sources.list.d/pgdg.list && \
    wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - && \
    apt-get update && \
    apt-get install -y postgresql-client-16 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*


WORKDIR /app
RUN go install github.com/air-verse/air@latest
RUN go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN go build -o main .


EXPOSE 8080
CMD ["air"]

# Production
FROM golang:1.23.0 AS production

WORKDIR /app

COPY go.mod go.sum ./

RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go production -o /safebase-backend

FROM alpine:latest

RUN apk --no-cache add ca-certificates

USER 1000:1000

COPY --from=production /safebase-backend /safebase-backend

EXPOSE 8080

ENTRYPOINT ["/safebase-backend"]