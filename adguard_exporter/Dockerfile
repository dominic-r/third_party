# Stage 1: Get CA certificates from alpine
FROM alpine:3.21.3@sha256:a8560b36e8b8210634f77d9f7f9efd7ffa463e380b75e2e74aff4511df3ef88c AS certs
RUN apk add ca-certificates

# Stage 2: Build the adguard-exporter
FROM golang:1.24.3@sha256:02a22753ab3426d91ba5ba6f4dfb4ac2454f19b05afdb18d61ab02cbf1a2dffe AS builder
WORKDIR /build
COPY . /build
RUN go mod download
RUN CGO_ENABLED=0 go build -a -o adguard-exporter main.go

# Stage 3: Final image
FROM alpine:3.21.3@sha256:a8560b36e8b8210634f77d9f7f9efd7ffa463e380b75e2e74aff4511df3ef88c

# Copy the CA certificates and the built binary
COPY --from=certs /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
COPY --from=builder /build/adguard-exporter /adguard-exporter

# Set the user and entrypoint
USER 65532:65532
ENTRYPOINT ["/adguard-exporter"]
