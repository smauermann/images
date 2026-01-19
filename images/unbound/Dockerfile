FROM cgr.dev/chainguard/wolfi-base:latest

# renovate: datasource=apk depName=unbound repository=https://packages.wolfi.dev/os
ARG UNBOUND_VERSION=1.24.2

RUN apk add --no-cache \
  unbound=~${UNBOUND_VERSION} \
  ca-certificates \
  bind-tools \
  dnssec-root \
  && unbound-anchor -a /usr/share/dnssec-root/trusted-key.key || true

EXPOSE 53/tcp 53/udp

CMD ["unbound", "-d"]
