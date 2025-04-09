# 什么是distrobuilder？

`distrobuilder` 是专为LXC和Incus容器设计的镜像构建工具，用于构建发布在[官方镜像服务器](https://images.linuxcontainers.org)上的所有标准镜像。

## 工作原理
通过YAML格式的镜像定义文件，您可以配置：
- 镜像源地址
- 使用的包管理器
- 针对不同镜像变体/操作系统发行版/CPU架构的软件包管理方案
- 需要生成的额外文件
- 构建过程中执行的自定义操作指令

支持生成三种输出格式：
1. 纯净的根文件系统
2. Incus专用镜像
3. LXC兼容镜像

实时构建过程可查看：[镜像构建工作台](https://jenkins.linuxcontainers.org/view/Images/)

## 安装指南
稳定版压缩包请前往[下载中心](/distrobuilder/downloads)获取

或使用Go命令安装最新开发版：
```bash
go install -v -x github.com/lxc/distrobuilder/distrobuilder@latest

# 语言、许可与贡献
distrobuilder 使用 Go 语言开发，是遵循 Apache 2 许可证的自由软件。

贡献 distrobuilder 无需签署 CLA（贡献者许可协议）或其他类似法律文件，但我们要求所有提交都必须包含 Signed-off-by 签名（遵循 DCO - 开发者原创证书）。