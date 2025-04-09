# 什么是CGManager？

CGManager是一个通过简单D-Bus API管理所有cgroup的中央特权守护进程。它设计用于嵌套LXC容器，并能接受非特权请求（包括解析用户命名空间的UID/GID）。

!!! 注意
    CGManager自2014年4月起在Ubuntu中作为LXC的默认组件使用，随后其他发行版在需要非特权容器支持时也开始采用。

    目前已被新版Linux内核中的CGroup命名空间功能取代。对于旧内核，LXCFS仍提供cgroupfs模拟方案，可作为CGManager的替代品，且与现有用户空间兼容性更好。

# 核心组件
## cgmanager主守护进程
运行在宿主机上，将cgroupfs挂载到独立的挂载命名空间（对宿主机不可见），绑定`/sys/fs/cgroup/cgmanager/sock`处理D-Bus请求，主要处理直接运行在宿主机上的客户端请求。

支持两种认证方式：
- 使用D-Bus + SCM凭证进行跨命名空间的uid/gid/pid转换
- 对宿主机层面的查询使用简单"非认证"（仅初始ucred）D-Bus

## cgproxy代理守护进程
在以下两种情况运行：
1. 宿主机使用低于3.8的内核（不支持pidns附加）
2. 容器内部（仅运行cgproxy）

cgproxy本身不执行cgroup配置更改，而是将请求代理转发给主cgmanager进程。这使得进程可以通过标准D-Bus（如dbus-send）与`/sys/fs/cgroup/cgmanager/sock`通信。

## cgm命令行工具
通过D-Bus与服务交互的命令行工具，支持所有常规cgroup操作。

# 通信协议
采用D-Bus通信。建议外部客户端使用标准D-Bus API而非SCM凭证协议（容易出错）。只需与`/sys/fs/cgroup/cgmanager/sock`交互即可。

注意：
- cgmanager API仅通过独立D-Bus socket提供
- 不需要依赖系统总线，无需运行dbus守护进程

[详细D-Bus API文档](/cgmanager/dbus-api/)

# 授权许可
- 主要代码：GNU LGPLv2.1+
- 部分二进制文件：GNU GPLv2
- 默认项目许可：GNU LGPLv2.1+

# 支持政策
稳定版支持依赖各Linux发行版自身的安全更新机制。