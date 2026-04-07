# 通过构建参数传递基础镜像和 Node.js 版本
ARG BASE_IMAGE=electronuserland/builder:20-wine-03.25
ARG NODE_VERSION=22

FROM ${BASE_IMAGE}

# 安装指定版本的 Node.js（使用官方二进制包）
RUN ARCH=$(uname -m) \
    && if [ "$ARCH" = "x86_64" ]; then ARCH="x64"; elif [ "$ARCH" = "aarch64" ]; then ARCH="arm64"; fi \
    # 改进 JS 逻辑：增加错误检查，并确保匹配到正确的大版本
    && echo "const d=JSON.parse(require('fs').readFileSync('/dev/stdin','utf8')); \
       const v=d.find(x => x.version.startsWith('v' + process.argv[1] + '.')); \
       if(!v) { console.error('Version not found'); process.exit(1); } \
       console.log(v.version.slice(1));" > /tmp/get_node_ver.js \
    # 执行解析
    && NODE_VERSION_FULL=$(curl -fsSL https://nodejs.org/dist/index.json | node /tmp/get_node_ver.js "${NODE_VERSION}") \
    && echo "Installing Node.js v${NODE_VERSION_FULL} for ${ARCH}" \
    # 下载并解压
    && curl -fsSL "https://nodejs.org/dist/v${NODE_VERSION_FULL}/node-v${NODE_VERSION_FULL}-linux-${ARCH}.tar.xz" | tar -xJ -C /usr/local --strip-components=1 \
    # 清理并验证
    && rm /tmp/get_node_ver.js \
    && node -v && npm -v

# 安装 pnpm
RUN npm install -g pnpm \
  && pnpm -v
