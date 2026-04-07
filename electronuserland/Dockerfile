# 通过构建参数传递基础镜像和 Node.js 版本
ARG BASE_IMAGE=electronuserland/builder:20-wine-03.25
ARG NODE_VERSION=22

FROM ${BASE_IMAGE}

# 使用 n 包升级到指定版本的 Node.js
RUN npm install -g n \
  && n ${NODE_VERSION} \
  && node -v \
  && npm -v \
  && rm -rf /usr/local/n /tmp/*

# 安装 pnpm
RUN npm install -g pnpm \
  && pnpm -v
