---
title: "openwrt 使用USB存储"
date: <span class="timestamp-wrapper"><span class="timestamp">&lt;2019-07-11 四 00:33&gt;</span></span>
layout: post
categories: 
- openwrt
tags: 
- linux 
- openwrt
---

# Table of Contents

1.  [安装支持外部USB存储功能](#org481c04c)
2.  [自动挂载分区](#org9b99096)
3.  [配置openwrt 根分区存储到USB存储。](#org17ed515)
    1.  [步骤](#orga6ea50d)
    2.  [配置/overlay 挂载](#org96fb489)
4.  [大功告成！](#orga8b1e4a)


<a id="org481c04c"></a>

# 安装支持外部USB存储功能

{% highlight shell %}
# 存储USB可以先分好区再插进去使用。这里讲ext4分区。

opkg update
opkg install kmod-usb-storage
opkg install block-mount
opkg install kmod-fs-ext4

# 查看存储设备
block info | grep "/dev/sd"


# 分区可安装gdisk
# opkg install gdisk

# 可选 格式化操作
# opkg install e2fsprogs
# opkg install kmod-fs-ext4
# mkfs.ext4 /dev/sda1
{% endhighlight %}


<a id="org9b99096"></a>

# 自动挂载分区

{% highlight shell %}
# 检测并生成配置条目，存入fstab
block detect | uci import fstab

# 设置自动挂载
uci set fstab.@mount[-1].enabled='1'
uci commit fstab

# 可选， 用于开启自动检查fs
uci set fstab.@global[0].check_fs='1'
uci commit fstab

# 查看挂载内容
uci show fstab
{% endhighlight %}


<a id="org17ed515"></a>

# 配置openwrt 根分区存储到USB存储。

主要目的用于扩展存储使用空间。


<a id="orga6ea50d"></a>

## 步骤

{% highlight shell %}
# 挂载外部存储
mount /dev/sda1 /mnt

# 拷贝根分区已有数据
tar -C /overlay/ -c . -f - | tar -C /mnt/ -xf -

# 同步并卸载 /mnt
sync && umount /dev/sda1

# 检测条目并写入fstab
block detect > /etc/config/fstab
{% endhighlight %}


<a id="org96fb489"></a>

## 配置/overlay 挂载

-   vi /etc/config/fstab
    
    {% highlight shell %}
    config 'global'
           option  anon_swap       '0'
           option  anon_mount      '0'
           option  auto_swap       '1'
           option  auto_mount      '1'
           option  delay_root      '5'
           option  check_fs        '0'
    
    config 'mount'
           option  target  '/overlay'
           option  uuid    '7669178c-3f77-4fb1-b421-6ec6f61be672'
           option  enabled '1'
    {% endhighlight %}

-   /etc/init.d/fstab enable

-   readlink -f /etc/rc.d/\*fstab

-   reboot


<a id="orga8b1e4a"></a>

# 大功告成！
