# 通过构建参数传递基础镜像
ARG BASE_IMAGE=centos:7

FROM ${BASE_IMAGE}

USER root

# CentOS 7 已停止维护，切换到 Vault 归档源
RUN sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*.repo && \
    sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*.repo

# 安装必要的开发库
RUN yum update -y && \
    yum install -y \
    gcc \
    glibc-devel \
    zlib-devel \
    fontconfig && \
    yum clean all && \
    rm -rf /var/cache/yum/*
