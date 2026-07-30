# Custom ARC runner image approximating GitHub-hosted ubuntu-latest
# for Texera CI. Built by .github/workflows/build-arc-runner-image.yml,
# consumed by the arc-linux runner scale set (containerMode: dind).
FROM ghcr.io/actions/actions-runner:latest

USER root
ENV DEBIAN_FRONTEND=noninteractive

# Core toolchain the workflows assume from ubuntu-latest:
# - build-essential/make: skywalking-eyes, native pip builds
# - postgresql-client: psql init steps in build.yml
# - locales/libicu-dev: zonky embedded Postgres in amber tests
# - lsof/iproute2/procps: bin/local-dev.sh smoke tests
RUN apt-get update && apt-get install -y --no-install-recommends \
      build-essential \
      sudo \
      git git-lfs \
      curl wget ca-certificates gnupg \
      jq \
      zip unzip xz-utils bzip2 \
      tar rsync file \
      openssh-client \
      python3 python3-pip python3-venv \
      postgresql-client \
      locales libicu-dev \
      lsof iproute2 procps netcat-openbsd socat \
      libgbm1 libnss3 fonts-liberation \
    && (apt-get install -y --no-install-recommends libasound2t64 \
        || apt-get install -y --no-install-recommends libasound2) \
    && locale-gen en_US.UTF-8 \
    && rm -rf /var/lib/apt/lists/*

ENV LANG=en_US.UTF-8 LC_ALL=en_US.UTF-8

# Passwordless sudo, same as GitHub-hosted runners (protoc install,
# playwright install --with-deps, apt steps in workflows).
RUN echo "runner ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/runner \
    && chmod 0440 /etc/sudoers.d/runner

# Go — required by apache/skywalking-eyes (`make install` runs go install).
# GOPATH bin and ~/.local/bin are on PATH like on GitHub-hosted runners
# (skywalking-eyes invokes license-eye from ~/go/bin after go install).
ARG GO_VERSION=1.24.5
RUN curl -fsSL "https://go.dev/dl/go${GO_VERSION}.linux-amd64.tar.gz" | tar -C /usr/local -xz
ENV PATH="/usr/local/go/bin:/home/runner/go/bin:/home/runner/.local/bin:${PATH}"

# Google Chrome — frontend karma ChromeHeadless tests.
RUN curl -fsSL https://dl.google.com/linux/linux_signing_key.pub \
      | gpg --dearmor -o /usr/share/keyrings/google-chrome.gpg \
    && echo "deb [arch=amd64 signed-by=/usr/share/keyrings/google-chrome.gpg] https://dl.google.com/linux/chrome/deb/ stable main" \
      > /etc/apt/sources.list.d/google-chrome.list \
    && apt-get update && apt-get install -y --no-install-recommends google-chrome-stable \
    && rm -rf /var/lib/apt/lists/*
ENV CHROME_BIN=/usr/bin/google-chrome

USER runner
