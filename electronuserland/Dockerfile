# 通过构建参数传递基础镜像和 Node.js 版本
ARG BASE_IMAGE=electronuserland/builder:20-wine-03.25
ARG NODE_VERSION=22

FROM ${BASE_IMAGE}

# 安装指定版本的 Node.js
RUN apt-get update \
  && apt-get install -y curl gnupg ca-certificates \
  && curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | gpg --dearmor -o /usr/share/keyrings/nodesource.gpg \
  && echo "deb [signed-by=/usr/share/keyrings/nodesource.gpg] https://deb.nodesource.com/node_${NODE_VERSION}.x nodistro main" > /etc/apt/sources.list.d/nodesource.list \
  && apt-get update \
  && apt-get install -y nodejs \
  && node -v \
  && npm -v \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/keyrings/nodesource.gpg

# 安装 pnpm
RUN npm install -g pnpm \
  && pnpm -v
