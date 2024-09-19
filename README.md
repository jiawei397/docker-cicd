# 利用 GitHub 流水线构建镜像

## Rust

tag 标签为：`rust-alpine1.70-0`.

## npm

- 18: node:18-alpine3.17
- 20: node:20-alpine3.20

tag 标签为：`npm_18-alpine3.17_18.0.5-alpine` 或 `npm_20-alpine3.20_20.0.0-alpine`。
以`npm_18-alpine3.17_18.0.4-alpine`为例，以下划线连接，第 1 段是 npm，第 2 段是基础镜像名，也就是下面的 BASE_IMAGE，第 3 段是要打的镜像的 tag。
最终推送的镜像为：`node:18.0.4-alpine`。

```shell
git tag npm_18-alpine3.17_18.0.5-alpine
git push origin npm_18-alpine3.17_18.0.5-alpine
```
