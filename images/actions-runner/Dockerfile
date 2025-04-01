ARG RUNNER_VERSION=2.323.0
ARG ARGOCD_VERSION=2.14.3

FROM --platform=amd64 bitnami/argo-cd:${ARGOCD_VERSION} AS argocd
FROM --platform=amd64 ghcr.io/actions/actions-runner:${RUNNER_VERSION}

ENV DEBCONF_NONINTERACTIVE_SEEN=true \
    DEBIAN_FRONTEND="noninteractive" \
    APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=DontWarn

USER root

RUN \
    apt-get update \
    && \
    apt-get install -y --no-install-recommends --no-install-suggests \
        ca-certificates \
        gcc \
        wget \
        zstd \
    && rm -rf /var/lib/apt/lists/*

COPY --from=argocd /opt/bitnami/argo-cd/bin/argocd /usr/local/bin/argocd

USER runner
