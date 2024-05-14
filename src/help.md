# Help

## 文件系统制作

```shell
sudo debootstrap  --variant=minbase --include=whiptail,ca-certificates,tzdata buster rootfs-debian https://mirrors.ustc.edu.cn/debian/
```

### 安装软件包

```shell
apt install udev vim net-tools iputils-ping  ethtool ifupdown rsyslog bash-completion iperf3  kmod pciutils -y
```

### 安装驱动

linux 目录下

```shell
make LLVM=1 INSTALL_MOD_PATH=/home/zhourui/rootfs-debian modules_install
```



### 挂载设备

```shel
mount -t proc proc /proc
mount sysfs /sys -t sysfs
modprobe e1000-for-linux
ip addr add 192.168.1.129/24 dev eth0
ip link set eth0 up
ip route add default via 192.168.1.1
```
