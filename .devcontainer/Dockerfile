FROM mcr.microsoft.com/devcontainers/base:latest

# https://mise.jdx.dev/mise-cookbook/docker.html
RUN apt-get update  \
    && apt-get -y --no-install-recommends install  \
    # install any other dependencies you might need
    # sudo \
    # curl \
    git \
    # ca-certificates \
    # build-essential \
    && rm -rf /var/lib/apt/lists/*

SHELL ["/bin/bash", "-o", "pipefail", "-c"]
ENV MISE_DATA_DIR="/mise"
ENV MISE_CONFIG_DIR="/mise"
ENV MISE_CACHE_DIR="/mise/cache"
ENV MISE_INSTALL_PATH="/usr/local/bin/mise"
ENV PATH="/mise/shims:$PATH"
# ENV MISE_VERSION="..."

RUN curl https://mise.run | sh
