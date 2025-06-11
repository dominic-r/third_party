FROM golang:1.24.4-bookworm@sha256:97162678719a516c12d5fb4b08266ab04802358cff63697ab1584be29ee8995c AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

ENV CGO_ENABLED=0
RUN go build -o /out/unbound_exporter ./...

FROM gcr.io/distroless/static-debian12@sha256:d9f9472a8f4541368192d714a995eb1a99bab1f7071fc8bde261d7eda3b667d8

COPY --from=builder /out/unbound_exporter /

ENTRYPOINT ["/unbound_exporter"]
