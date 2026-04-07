# 通过构建参数传递基础镜像和 Node.js 版本
ARG BASE_IMAGE=electronuserland/builder:20-wine-03.25
ARG NODE_VERSION=22

FROM ${BASE_IMAGE}

# 安装指定版本的 Node.js（使用官方二进制包）
RUN ARCH=$(uname -m) \
  && if [ "$ARCH" = "x86_64" ]; then ARCH="x64"; elif [ "$ARCH" = "aarch64" ]; then ARCH="arm64"; fi \
  && NODE_VERSION_FULL=$(node -p "fetch('https://nodejs.org/dist/index.json').then(r=>r.json()).then(d=>d.find(v=>v.version.startsWith('v${NODE_VERSION}.')).version.slice(1))") \
  && echo "Installing Node.js v${NODE_VERSION_FULL} for ${ARCH}" \
  && curl -fsSL "https://nodejs.org/dist/v${NODE_VERSION_FULL}/node-v${NODE_VERSION_FULL}-linux-${ARCH}.tar.xz" | tar -xJ -C /usr/local --strip-components=1 \
  && node -v \
  && npm -v

# 安装 pnpm
RUN npm install -g pnpm \
  && pnpm -v
