FROM golang:1.24.3-bookworm@sha256:573d8655afbdb5fb461aaf517e661fa8207633f01d5ec1d6e82546e53d7342b2 AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

ENV CGO_ENABLED=0
RUN go build -o /out/unbound_exporter ./...

FROM gcr.io/distroless/static-debian12@sha256:d9f9472a8f4541368192d714a995eb1a99bab1f7071fc8bde261d7eda3b667d8

COPY --from=builder /out/unbound_exporter /

ENTRYPOINT ["/unbound_exporter"]
