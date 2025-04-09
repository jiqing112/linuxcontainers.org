# 2014-01-10 更新
<!--
The cgmanager socket has been moved to /sys/fs/cgroup/manager/sock.
-->
CGManager套接字路径已变更为`/sys/fs/cgroup/manager/sock`

<!--
The proxy moves that to /sys/fs/cgroup/manager.lower/sock then offers its
own service over /sys/fs/cgroup/manager/sock. This allows a container to
to have /sys/fs/cgroup/manager bind-mounted instead of the socket
itself, allowing it to recover after the cgmanager on the host restarts.
-->
代理服务会将原始套接字移至`/sys/fs/cgroup/manager.lower/sock`，并通过`/sys/fs/cgroup/manager/sock`提供新服务。这一改进使得：
- 容器可以绑定挂载整个`/sys/fs/cgroup/manager`目录而非单个套接字文件
- 当宿主机cgmanager重启后，容器能够自动恢复连接

# 2014-01-09 更新
<!--
The scm handling has been reworked. Now all \*Scm dbus transactions
complete as soon as the server receives the unix fd. It then reads the
scm credentials (asynchronously) over the unix fd and sends the results
to the client over the same fd.
-->
SCM凭证处理机制重构：
- 所有\*Scm类型的D-Bus事务现将在服务端收到Unix文件描述符后立即完成
- 凭证读取改为异步方式，通过同一文件描述符进行凭证验证和结果返回