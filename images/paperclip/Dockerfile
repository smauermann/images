# Paperclip doesn't publish semver tags yet, only `latest` and per-commit
# `sha-<hash>` tags, so we pin to a specific commit tag for reproducibility.
# renovate: datasource=docker depName=ghcr.io/paperclipai/paperclip
ARG PAPERCLIP_VERSION=sha-903886b

FROM ghcr.io/paperclipai/paperclip:${PAPERCLIP_VERSION}

USER root

# Local adapters (Claude Code, Codex) spawn these CLIs as subprocesses on
# the same container as the Paperclip server, so they need to be installed
# here rather than reached over the network.
RUN npm install -g @anthropic-ai/claude-code @openai/codex \
    && rm -rf /root/.npm

USER 1000:1000
