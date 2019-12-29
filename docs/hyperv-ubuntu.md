# [Cloud开发笔记本](../README.md)

## Hyper-V中安装Ubuntu虚拟机

### 1. Hyper-V是Windows操作系统下通用选择

* Windows设备中一些CPU不支持KVM以及VisualBox，如果CPU不支持则需要考虑使用Hyper-V，也可以使用VMWare。

### 2. 配置网络

* 使用外部网卡：如果宿主机配置了VPN连接内网，在虚拟机中可以利用外部网卡使得宿主机与虚拟机在同一网段。此时，配置`route`可以直接共享VPN。

* 禁用IPv6：在使用外部网卡后，由于默认启用了IPv6导致虚拟机无法正常访问外网，可以通过禁用IPv6的方式解决网络问题。

    a. 使用以下命令编辑配置文件

    ```
    sudo gedit /etc/sysctl.conf
    ```

    b. 文件末尾添加以下内容

    ```
    net.ipv6.conf.all.disable_ipv6=1
    net.ipv6.conf.default.disable_ipv6=1
    net.ipv6.conf.lo.disable_ipv6=1
    ```
  
    c. 重启sysctl
    ```
    sudo sysctl -p
    ```
