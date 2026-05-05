# renovate: datasource=docker depName=ghcr.io/openclaw/openclaw
ARG OPENCLAW_VERSION=2026.5.4

FROM ghcr.io/openclaw/openclaw:${OPENCLAW_VERSION}

USER root

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        chromium \
        ca-certificates \
        fonts-liberation \
    && rm -rf /var/lib/apt/lists/*

USER node
