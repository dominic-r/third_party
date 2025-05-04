# Stage 1: Get CA certificates from alpine
FROM alpine:3.21.0 AS certs
RUN apk add ca-certificates

# Stage 2: Build the adguard-exporter
FROM golang:1.24.0 AS builder
WORKDIR /build
COPY . /build
RUN go mod download
RUN CGO_ENABLED=0 go build -a -o adguard-exporter main.go

# Stage 3: Final image
FROM alpine:3.21.0

# Copy the CA certificates and the built binary
COPY --from=certs /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
COPY --from=builder /build/adguard-exporter /adguard-exporter

# Set the user and entrypoint
USER 65532:65532
ENTRYPOINT ["/adguard-exporter"]
