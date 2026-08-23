FROM otel/opentelemetry-collector-contrib:latest AS collector
FROM prom/prometheus:latest AS prometheus
FROM alpine:latest

RUN apk add --no-cache supervisor ca-certificates

COPY --from=collector /otelcol-contrib /usr/bin/otelcol-contrib
COPY --from=prometheus /bin/prometheus /usr/bin/prometheus

COPY otel-collector-config.yaml /etc/otelcol/config.yaml
COPY prometheus.yml /etc/prometheus/prometheus.yml
COPY supervisord.conf /etc/supervisord.conf

CMD ["supervisord", "-c", "/etc/supervisord.conf"]