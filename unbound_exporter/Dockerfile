FROM golang:1.24.3-bookworm@sha256:f6c2de2175f4371e842a74185ee0c2cf74c8dc34fb03e68474956f5cc34676bb AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

ENV CGO_ENABLED=0
RUN go build -o /out/unbound_exporter ./...

FROM gcr.io/distroless/static-debian12@sha256:d9f9472a8f4541368192d714a995eb1a99bab1f7071fc8bde261d7eda3b667d8

COPY --from=builder /out/unbound_exporter /

ENTRYPOINT ["/unbound_exporter"]
