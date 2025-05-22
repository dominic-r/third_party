FROM golang:1.24.3-bookworm@sha256:212d7b393369e37fb7009a7f6fe30b20fd0d05ee1539d0de116b7c6100061cf4 AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

ENV CGO_ENABLED=0
RUN go build -o /out/unbound_exporter ./...

FROM gcr.io/distroless/static-debian12@sha256:d9f9472a8f4541368192d714a995eb1a99bab1f7071fc8bde261d7eda3b667d8

COPY --from=builder /out/unbound_exporter /

ENTRYPOINT ["/unbound_exporter"]
