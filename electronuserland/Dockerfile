# 通过构建参数传递基础镜像和 Node.js 完整版本
ARG BASE_IMAGE=electronuserland/builder:20-wine-03.25
ARG NODE_VERSION=22.22.0

FROM ${BASE_IMAGE}

ARG NODE_VERSION
USER root

# 合并 RUN 指令，减少镜像层数，清理冗余文件
RUN set -e; \
    # 1. 预清理：删除旧版 Node 的残留，腾出空间
    rm -rf /usr/local/bin/node /usr/local/bin/npm /usr/local/bin/npx /usr/local/lib/node_modules /usr/local/include/node; \
    \
    # 2. 下载并安装新版 Node
    ARCH=$(uname -m | sed 's/x86_64/x64/;s/aarch64/arm64/'); \
    curl -fsSL "https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-${ARCH}.tar.xz" | tar -xJ -C /usr/local --strip-components=1; \
    \
    # 3. 配置 npm 并安装 pnpm (内网建议直接指定 registry)
    npm install -g pnpm; \
    \
    # 4. 关键优化：清理 npm/pnpm 缓存
    # 这些缓存文件在 CI 运行环境中毫无用处，只会白白增加镜像体积（通常几百MB）
    npm cache clean --force; \
    \
    # 5. 验证
    node -v && npm -v && pnpm -v
