# 在Ubuntu和Debian中使用CGManager

<!--
In Ubuntu, installing cgmanager and the cgm program can be done with:
-->
在Ubuntu中，可以通过以下命令安装cgmanager和cgm工具：

    sudo apt-get install cgmanager cgmanager-utils

<!--
If logind has not placed you into your own cgroup, you can then do so using:
-->
如果logind没有将您放入自己的cgroup中，可以执行以下命令：

    sudo cgm create all me
    sudo cgm chown all me $(id -u) $(id -g)
    sudo cgm movepid all me $$

# 在其他发行版上构建CGManager
<!--
If you are running another distribution, you can install it by hand using:
-->
如果您使用其他发行版，可以手动安装：

    git clone git://github.com/lxc/cgmanager
    sh bootstrap.sh
    ./configure --prefix=/
    make
    sudo make install
    sudo /sbin/cgmanager --debug -m name=systemd

# 在LXC容器内使用CGManager
<!--
To use cgmanager in containers, you need to tell lxc to bind mount the
cgmanager socket into the container by adding the following line into
the container configuration file (e.g. /var/lib/lxc/container/config).
-->
要在容器内使用cgmanager，您需要在容器配置文件（如/var/lib/lxc/container/config）中添加以下行，将cgmanager套接字绑定挂载到容器中：

    lxc.mount.auto = cgroup