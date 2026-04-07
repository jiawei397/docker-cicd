# 通过构建参数传递基础镜像和 Node.js 完整版本
ARG BASE_IMAGE=electronuserland/builder:20-wine-03.25
ARG NODE_VERSION=22.22.0

FROM ${BASE_IMAGE}

ARG NODE_VERSION

USER root

RUN rm -rf /usr/local/bin/node \
           /usr/local/bin/npm \
           /usr/local/lib/node_modules

# 安装指定版本的 Node.js（使用官方二进制包）
RUN set -e; \
    ARCH=$(uname -m | sed 's/x86_64/x64/;s/aarch64/arm64/'); \
    echo "Installing Node.js v${NODE_VERSION} for ${ARCH}..." && \
    curl -fsSL "https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-${ARCH}.tar.xz" -o /tmp/node.tar.xz && \
    tar -xJf /tmp/node.tar.xz -C /usr/local --strip-components=1 && \
    rm /tmp/node.tar.xz && \
    echo "Successfully installed Node.js $(node -v)" && \
    npm -v 
RUN npm install -g pnpm
