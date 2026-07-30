# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.

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

# Temurin JDK 17 — preinstalled on GitHub-hosted images; bin/local-dev.sh
# (infra job) probes for a JDK 17 install without running setup-java.
RUN curl -fsSL https://packages.adoptium.net/artifactory/api/gpg/key/public \
      | gpg --dearmor -o /usr/share/keyrings/adoptium.gpg \
    && echo "deb [signed-by=/usr/share/keyrings/adoptium.gpg] https://packages.adoptium.net/artifactory/deb $(. /etc/os-release && echo $VERSION_CODENAME) main" \
      > /etc/apt/sources.list.d/adoptium.list \
    && apt-get update && apt-get install -y --no-install-recommends temurin-17-jdk \
    && rm -rf /var/lib/apt/lists/*
ENV JAVA_HOME_17_X64=/usr/lib/jvm/temurin-17-jdk-amd64

# Google Chrome — frontend karma ChromeHeadless tests.
RUN curl -fsSL https://dl.google.com/linux/linux_signing_key.pub \
      | gpg --dearmor -o /usr/share/keyrings/google-chrome.gpg \
    && echo "deb [arch=amd64 signed-by=/usr/share/keyrings/google-chrome.gpg] https://dl.google.com/linux/chrome/deb/ stable main" \
      > /etc/apt/sources.list.d/google-chrome.list \
    && apt-get update && apt-get install -y --no-install-recommends google-chrome-stable \
    && rm -rf /var/lib/apt/lists/*
ENV CHROME_BIN=/usr/bin/google-chrome

# GitHub-hosted images keep /usr/local user-writable; tools like
# skywalking-eyes `cp` binaries straight into /usr/local/bin without sudo.
RUN chown -R runner:runner /usr/local/bin /usr/local/include /usr/local/lib /usr/local/share

USER runner
