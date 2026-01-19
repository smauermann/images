FROM cgr.dev/chainguard/wolfi-base:latest

# renovate: datasource=github-releases depName=NLnetLabs/unbound
ARG UNBOUND_VERSION=1.24.2

RUN apk add --no-cache \
  unbound=~${UNBOUND_VERSION} \
  ca-certificates \
  bind-tools \
  dnssec-root \
  && unbound-anchor -a /usr/share/dnssec-root/trusted-key.key || true

EXPOSE 53/tcp 53/udp

CMD ["unbound", "-d"]
