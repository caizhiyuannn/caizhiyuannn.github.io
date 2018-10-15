---
title: Linux 启动引导记录
date: 2016-06-16 20:00
categories: linux
tags: linux grub uefi
---

# Linux 启动相关的学习笔记

## Grub2 的手动引导记录
- 当系统出现引导问题时，出现到grub 的恢复模式无法正常进入系统。
- 一般情况下，可以通过手动引导进入系统进行修复
- `ls` 查看系统磁盘情况。
- `set` 查看设置的变量是否正确。  
	一般查看**root**和**prefix** 的变量值
- `set root` 和 `set prefix`  进行配置值
- `linux /boot/vmlinux* ro root=/dev/sdx` 指定加载的linux内核文件及根目录
- `initrd /boot/initrd* ` 指定初始化的压缩文件。
- `boot` 进行引导


## Grub2 的EFI 配置
- 配置EFI 引导系统，首先需要uefi 引导的支持。
- 同时可以使用gpt分区
- linux 配置EFI 所用到的工具 **efibootmgr** 、 **efivar** 、 **grub2**
- **grub2-install** 的使用，`grub2-install --target=x86_64-efi  --efi-directory=/boot/efi`  
  grub2-install 命令将自动创建EFI目录到/boot/efi/目录下。并且配置efi的引导记录
- **efibootmgr** 命令主要是用来查看efi 的引导记录。或者创建引导记录  
  `efibootmgr -v` -- 查看记录  
  `efibootmgr -b xxxx -B` -- 删除指定的引导记录  
  `efibootmgr -c -d /dev/sda -p 2 -L "Gentoo" -l "\EFI\boot\bootx64.efi"`  
  表示在/dev/sda 的第二个分区下创建名为Gentoo 的引导记录，指定执行bootx64.efi文件
- 一般情况下，efi引导可直接引导系统下对应的grubx64.efi 文件。由efi
