---
title: Linux交叉编译
# subtitle: Linux交叉编译解决办法。

# Summary for listings and search engines
summary: Linux交叉编译解决办法。

# Link this post with a project
projects: []

# Date published
date: "2020-12-13T00:00:00Z"

# Date updated
lastmod: "2020-12-13T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

toc: true

pager: true

show_related: true

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: "Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)"
  focal_point: ""
  placement: 2
  preview_only: false

authors:
  - admin

tags:
  - Linux
  - 交叉编译

categories:
  - Linux
---

## 前提

Linux 物理机内核版本需高于 `4.18` 。如下：

```bash
[root@test ~]$ uname -a
Linux test 3.10.0-693.el7.x86_64 #1 SMP Tue Aug 22 21:09:27 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux
```

## 操作步骤

### 安装交叉编译工具

用于编译 arm64 版本程序

1. 下载[交叉编译工具](https://releases.linaro.org/components/toolchain/binaries/4.9-2017.01/aarch64-linux-gnu/), 这里选择文件 `gcc-linaro-4.9.4-2017.01-x86_64_aarch64-linux-gnu.tar.xz` 下载
2. 新建安装目录

   ```bash
   mkdir -p /usr/local/ARM-toolchain
   ```

3. 将安装包解压到该目录下

   ```bash
   tar -xf gcc-linaro-4.9.4-2017.01-x86_64_aarch64-linux-gnu.tar.xz -C /usr/local/ARM-toolchain/
   ```

4. 修改 `/etc/bash.bashrc` 文件，加入如下配置

   ```bash
   # Add ARM toolschain path
   if [ -d /usr/local/ARM-toolchain/gcc-linaro-4.9.4-2017.01-x86_64_aarch64-linux-gnu/bin ] ; then
   PATH=/usr/local/ARM-toolchain/gcc-linaro-4.9.4-2017.01-x86_64_aarch64-linux-gnu/bin:"${PATH}"
   fi
   ```

5. 执行 `source /etc/bash.bashrc`，使配置生效。
6. 执行 `aarch64-linux-gnu-gcc -v` 测试是否可用。
7. 此后在该系统下可指定使用 `aarch64-linux-gnu-gcc` 作为交叉编译器
8. 进入到目标项目目录下，执行命令 `make -xx` 编译 arm 版本程序。

### 安装 docker 版的 qemu

用于运行测试或打包镜像

1. 下载安装包： https://github.com/multiarch/qemu-user-static
2. 安装官方文档执行如下操作，安装配置模拟环境：

   ```bash
   uname -m

   # 返回 x86_64

   docker run --rm -t arm64v8/ubuntu uname -m standard_init_linux.go:211: exec user process caused "exec format error"

   docker run --rm --privileged multiarch/qemu-user-static --reset -p yes

   docker run --rm -t arm64v8/ubuntu uname -m aarch64
   ```

3. 上面步骤完成后，即可在该系统下直接运行 arm64 版本的可执行文件。
4. 进入到目标项目目录下，执行命令 `make image -xx` 编译 arm 版本程序。
