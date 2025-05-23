FROM golang:latest as build

ARG TARGETARCH

ARG BUILDER_VERSION=0.113.0

RUN curl --proto '=https' --tlsv1.2 -fL -o bin/ocb \
    https://github.com/open-telemetry/opentelemetry-collector-releases/releases/download/cmd%2Fbuilder%2Fv${BUILDER_VERSION}/ocb_${BUILDER_VERSION}_linux_${TARGETARCH}
RUN chmod +x bin/ocb
WORKDIR /build

# Copy the manifest file and builds the Collector binary
# with the defined components
COPY ./manifest.yaml ./manifest.yaml
ENV GOARCH=$TARGETARCH
ENV CGO_ENABLED=0
RUN ocb --config ./manifest.yaml --output-path /build/_build

FROM alpine:3.20 as certs
RUN apk --update add ca-certificates

# Final step runs the custom Collector binary
# with its configuration file
FROM alpine:3.20

ARG USER_UID=10001
USER ${USER_UID}

COPY --from=certs /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
COPY --from=build --chmod=755 /build/_build/otelcol /otelcol
COPY ./otelcol-config.yaml /etc/otelcol-config.yaml
ENTRYPOINT ["/otelcol", "--config=/etc/otelcol-config.yaml"]
EXPOSE 4317 4318
