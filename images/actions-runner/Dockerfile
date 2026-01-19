# renovate: datasource=github-releases depName=actions/runner
ARG RUNNER_VERSION=2.331.0
# renovate: datasource=github-releases depName=argoproj/argo-cd
ARG ARGOCD_VERSION=v3.2.5

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

ARG ARGOCD_VERSION
RUN curl -sSL -o /usr/local/bin/argocd https://github.com/argoproj/argo-cd/releases/download/${ARGOCD_VERSION}/argocd-linux-amd64 \
    && chmod +x /usr/local/bin/argocd

USER runner

