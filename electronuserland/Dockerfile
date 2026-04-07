# 通过构建参数传递基础镜像和 Node.js 版本
ARG BASE_IMAGE=electronuserland/builder:20-wine-03.25
ARG NODE_VERSION=22

FROM ${BASE_IMAGE}

# 安装指定版本的 Node.js（使用官方二进制包）
RUN apt-get update \
  && apt-get install -y curl xz-utils \
  && ARCH=$(uname -m) \
  && if [ "$ARCH" = "x86_64" ]; then ARCH="x64"; elif [ "$ARCH" = "aarch64" ]; then ARCH="arm64"; fi \
  && NODE_FULL_VERSION=$(curl -s https://nodejs.org/dist/latest-v${NODE_VERSION}.x/ | grep -oP 'node-v${NODE_VERSION}\.[0-9]+\.[0-9]+' | head -1) \
  && curl -fsSL https://nodejs.org/dist/latest-v${NODE_VERSION}.x/${NODE_FULL_VERSION}-linux-${ARCH}.tar.xz | tar -xJ -C /usr/local --strip-components=1 \
  && node -v \
  && npm -v \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# 安装 pnpm
RUN npm install -g pnpm \
  && pnpm -v
