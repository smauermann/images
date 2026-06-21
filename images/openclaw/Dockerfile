# renovate: datasource=docker depName=ghcr.io/openclaw/openclaw
ARG OPENCLAW_VERSION=2026.6.9

FROM ghcr.io/openclaw/openclaw:${OPENCLAW_VERSION}

USER root

# renovate: datasource=custom.1password-cli depName=1password-cli
ARG OP_CLI_VERSION=v2.34.1

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        chromium \
        ca-certificates \
        fonts-liberation \
        curl \
        unzip \
    && ARCH=$(dpkg --print-architecture) \
    && curl -fsSL "https://cache.agilebits.com/dist/1P/op2/pkg/${OP_CLI_VERSION}/op_linux_${ARCH}_${OP_CLI_VERSION}.zip" \
        -o /tmp/op.zip \
    && unzip /tmp/op.zip op -d /usr/local/bin/ \
    && chmod +x /usr/local/bin/op \
    && rm /tmp/op.zip \
    && rm -rf /var/lib/apt/lists/*

USER node
