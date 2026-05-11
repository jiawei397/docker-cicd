# 通过构建参数传递基础镜像
ARG BASE_IMAGE=centos:7

FROM ${BASE_IMAGE}

USER root

# 安装必要的开发库
RUN yum update -y && \
    yum install -y \
    gcc \
    glibc-devel \
    zlib-devel \
    fontconfig && \
    yum clean all && \
    rm -rf /var/cache/yum/*
