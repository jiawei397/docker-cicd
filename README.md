# 利用GitHub流水线构建镜像

## Rust

tag标签为：`rust-alpine1.70-0`.

## npm

- 18: node:18-alpine3.17
- 20: node:20-alpine3.20

tag标签为：`npm_18-alpine3.17_18.0.5-alpine` 或 `npm_20-alpine3.20_20.0.0-alpine`

```shell
git tag npm_18-alpine3.17_18.0.5-alpine
git push origin npm_18-alpine3.17_18.0.5-alpine
```
