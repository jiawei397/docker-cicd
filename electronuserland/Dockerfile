# 通过构建参数传递基础镜像和 Node.js 版本
ARG BASE_IMAGE=electronuserland/builder:20-wine-03.25

FROM ${BASE_IMAGE}

ARG NODE_VERSION=22

# 安装指定版本的 Node.js（使用官方二进制包）
RUN set -e; \
    # 1. 修正架构转换逻辑
    ARCH=$(uname -m | sed 's/x86_64/x64/;s/aarch64/arm64/'); \
    \
    # 2. 这里的 ${NODE_VERSION} 现在能拿到了
    echo "Checking for latest Node.js v${NODE_VERSION}..." && \
    \
    # 获取版本号
    FULL_VERSION=$(curl -fsSL https://nodejs.org/dist/index.tab | grep -E "^v${NODE_VERSION}\." | head -n 1 | cut -f 1) && \
    \
    if [ -z "$FULL_VERSION" ]; then \
        echo "Error: Could not find a version starting with v${NODE_VERSION}"; \
        exit 1; \
    fi; \
    \
    echo "Found full version: ${FULL_VERSION}"; \
    \
    # 3. 下载并安装
    curl -fsSL "https://nodejs.org/dist/${FULL_VERSION}/node-${FULL_VERSION}-linux-${ARCH}.tar.xz" -o /tmp/node.tar.xz && \
    tar -xJf /tmp/node.tar.xz -C /usr/local --strip-components=1 && \
    \
    # 4. 验证与清理
    rm /tmp/node.tar.xz && \
    echo "Successfully installed Node.js $(node -v)" && \
    npm -v

# 安装 pnpm
RUN npm install -g pnpm \
  && pnpm -v
