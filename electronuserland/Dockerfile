# 通过构建参数传递基础镜像和 Node.js 版本
ARG BASE_IMAGE=electronuserland/builder:20-wine-03.25
ARG NODE_VERSION=22

FROM ${BASE_IMAGE}

# 安装指定版本的 Node.js（使用官方二进制包）
RUN set -e; \
    ARCH=$(uname -m | sed 's/x86_64/x64/;s/aarch64/arm64/'); \
    echo "Checking for latest Node.js v${NODE_VERSION}..." && \
    FULL_VERSION=$(curl -fsSL https://nodejs.org/dist/index.tab | awk -F'\t' 'NR>1 && $1 ~ /^v'"${NODE_VERSION}"'\./ {print $1; exit}') && \
    if [ -z "$FULL_VERSION" ]; then \
        echo "Error: Could not find a version starting with v${NODE_VERSION}"; \
        exit 1; \
    fi && \
    echo "Found full version: ${FULL_VERSION}" && \
    curl -fsSL "https://nodejs.org/dist/${FULL_VERSION}/node-${FULL_VERSION}-linux-${ARCH}.tar.xz" -o /tmp/node.tar.xz && \
    tar -xJf /tmp/node.tar.xz -C /usr/local --strip-components=1 && \
    rm /tmp/node.tar.xz && \
    echo "Successfully installed Node.js $(node -v)" && \
    npm -v

# 安装 pnpm
RUN npm install -g pnpm \
  && pnpm -v
