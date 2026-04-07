# 通过构建参数传递基础镜像和 Node.js 版本
ARG BASE_IMAGE=electronuserland/builder:20-wine-03.25
ARG NODE_VERSION=22

FROM ${BASE_IMAGE}

# 安装指定版本的 Node.js（使用官方二进制包）
RUN set -e; \
    # 自动获取架构 (x64 或 arm64)
    ARCH=$(uname -m | sed 's/x86_64/x64/;s/aarch64/arm64/'); \
    \
    # 2. 直接从官网 index.tab 获取最新小版本号 (tab文件比json更好解析)
    # index.tab 的第一列是版本号，形如 v22.14.0
    echo "Checking for latest Node.js v${NODE_VERSION}..." && \
    FULL_VERSION=$(curl -fsSL https://nodejs.org/dist/index.tab | grep -E "^v${NODE_VERSION}\." | head -n 1 | cut -f 1) && \
    \
    if [ -z "$FULL_VERSION" ]; then echo "Could not find version v${NODE_VERSION}"; exit 1; fi; \
    echo "Found full version: ${FULL_VERSION}"; \
    \
    # 3. 下载并解压到 /usr/local
    curl -fsSL "https://nodejs.org/dist/${FULL_VERSION}/node-${FULL_VERSION}-linux-${ARCH}.tar.xz" -o /tmp/node.tar.xz && \
    tar -xJf /tmp/node.tar.xz -C /usr/local --strip-components=1 && \
    \
    # 4. 清理
    rm /tmp/node.tar.xz && \
    node -v && npm -v

# 安装 pnpm
RUN npm install -g pnpm \
  && pnpm -v
