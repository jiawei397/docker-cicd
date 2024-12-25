# 利用 GitHub 流水线构建镜像

## Rust

### 基础镜像

tag 标签为：`rust-alpine1.70-0`.

到[这里](https://hub.docker.com/_/rust)找镜像。

- 71: 1.81.0-alpine3.20

tag标签为：`rust-alpine_1.81.0-alpine3.20_1`。中间部分`1.81.0-alpine3.20`是基础镜像，最后部分用来拼接tag。

最终镜像为：`rust:alpine1.81.0-1`


### 运行时镜像

对`alpine`的封装。

- alpine:3.20

tag标签为：`rust-runtime_3.20_1`，中间部分`3.20`是alpine的基础镜像，最后部分用来拼接tag。

最终镜像为：`rust-runtime-alpine:3.20-1`

## npm

到[这里](https://hub.docker.com/_/node/tags?page_size=&ordering=&name=20-alpine)找镜像。

- 18: node:18-alpine3.17
- 20: node:20-alpine3.20

tag 标签为：`npm_18-alpine3.17_18.0.5-alpine` 或 `npm_20-alpine3.20_20.0.0-alpine`。
以`npm_18-alpine3.17_18.0.4-alpine`为例，以下划线连接，第 1 段是 npm，第 2 段是基础镜像名，也就是下面的 BASE_IMAGE，第 3 段是要打的镜像的 tag。
最终推送的镜像为：`node:18.0.4-alpine`。

```shell
git tag npm_18-alpine3.17_18.0.5-alpine
git push origin npm_18-alpine3.17_18.0.5-alpine
```

## 原生镜像

比如我要拉取一个`electronuserland/builder:20-wine`镜像，那么我可以打个tag为：
`origin_electronuserland@builder@20-wine`，最终推送的镜像为：`electronuserland-builder:20-wine`。
