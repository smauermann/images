ARG RUNNER_VERSION=2.322.0
ARG ARGOCD_VERSION=2.14.2
ARG HELM_VERSION=3.17.1
ARG KUSTOMIZE_VERSION=v5.6.0

FROM --platform=amd64 bitnami/argo-cd:${ARGOCD_VERSION} AS argocd
FROM --platform=amd64 alpine/helm:${HELM_VERSION} AS helm
FROM --platform=amd64 registry.k8s.io/kustomize/kustomize:${KUSTOMIZE_VERSION} AS kustomize

FROM --platform=amd64 ghcr.io/actions/actions-runner:${RUNNER_VERSION}

ENV HOMEBREW_NO_ANALYTICS=1 \
    HOMEBREW_NO_ENV_HINTS=1 \
    HOMEBREW_NO_INSTALL_CLEANUP=1 \
    DEBCONF_NONINTERACTIVE_SEEN=true \
    DEBIAN_FRONTEND="noninteractive" \
    APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=DontWarn

USER root

RUN \
    apt-get update \
    && \
    apt-get install -y --no-install-recommends --no-install-suggests \
        ca-certificates \
        gcc \
        jo \
        moreutils \
        wget \
        zstd \
    && curl -fsSL -o /usr/local/bin/yq https://github.com/mikefarah/yq/releases/latest/download/yq_linux_amd64 \
    && chmod +x /usr/local/bin/yq \
    && rm -rf /var/lib/apt/lists/*

COPY --from=argocd /opt/bitnami/argo-cd/bin/argocd /usr/local/bin/argocd
COPY --from=helm /usr/bin/helm /usr/local/bin/helm
COPY --from=kustomize /app/kustomize /usr/local/bin/kustomize

USER runner

RUN /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
