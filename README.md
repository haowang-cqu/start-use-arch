# 开始使用 Arch Linux
> 这里记录 Arch Linux 使用过程中遇到过的问题

## Tips
### efi 引导多系统的配置
```bash
pacman -S intel-ucode os-prober grub efibootmgr
grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=GRUB
grub-mkconfig -o /boot/grub/grub.cfg
```
[ArchWiki](https://wiki.archlinux.org/index.php/GRUB_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))

os-prober：探测其他操作系统

### 交换文件的创建
```bash
dd if=/dev/zero of=/swapfile bs=1G count=8
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile
echo '/swapfile none swap defaults 0 0' >> /etc/fstab
```
[ArchWiki](https://wiki.archlinux.org/index.php/Swap_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))

这里我用 fallocate -l 8G /swapfile 创建交换文件时 swapon 会报错

### 挂载 NTFS 格式的磁盘
```bash
sudo pacman -S ntfs-3g
```
[ArchWiki](https://wiki.archlinux.org/index.php/NTFS-3G_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))

ntfs-3g：提供ntfs文件系统的读写功能

### 开机启动网络管理器和蓝牙
```bash
systemctl enable NetworkManager
systemctl enable bluetooth
```
安装好kde后这两个服务并没有被设置为开机自启动

### 安装 .pacman 文件
```bash
yay -U xxx.pacman
```
