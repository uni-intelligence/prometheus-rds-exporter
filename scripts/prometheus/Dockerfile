ARG GO_VERSION="1.25"
ARG DISTROLESS_VERSION="static-debian12:nonroot"

FROM golang:${GO_VERSION} AS builder
WORKDIR /build
COPY go.mod go.sum ./
RUN go mod download
COPY . .
HEALTHCHECK NONE
RUN make build

FROM gcr.io/distroless/${DISTROLESS_VERSION}
COPY --from=builder /build/prometheus-rds-exporter /home/nonroot/prometheus-rds-exporter
HEALTHCHECK NONE
ENTRYPOINT ["/home/nonroot/prometheus-rds-exporter"]
