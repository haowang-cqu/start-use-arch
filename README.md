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

这里用 fallocate -l 8G /swapfile 创建交换文件时 swapon 会报错

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

### github相关域名无法正常访问
编辑/etc/hosts，添加如下内容
```bash
199.232.68.133  githubusercontent.com
199.232.68.133  raw.githubusercontent.com
140.82.114.4    github.com
```
获取域名所对应的ip地址[ipaddress.com](ipaddress.com)

### Discover 软件中心无法工作

缺少相应的可选依赖，使用 `pacman -Si` 查看可选依赖并安装

packagekit-qt5: to manage packages from Arch Linux repositories
flatpak: Flatpak packages support
fwupd: firmware update support

```bash
sudo pacman -S packagekit-qt5 flatpak fwupd
```

### 音频问题

[ArchWiki](https://wiki.archlinux.org/index.php/PulseAudio_(简体中文))

### WPS
```bash
sudo pacman -S wps-office-cn wps-office-mime-cn wps-office-mui-zh-cn ttf-wps-fonts
```

### 安装字体

```bash
# 带nerd font补丁的终端等宽字体
sudo pacman -S nerd-fonts-meslo-lg
# noto 全系字体
sudo pacman -S noto-fonts noto-fonts-cjk noto-fonts-emoji
# 带nerd font补丁的fira code
sudo pacman -S nerd-fonts-fira-code
```

### qq-linux 闪退
修改/usr/share/applications/qq.desktop
```
Exec=qq --no-sandbox %U
```

### zsh 插件安装

- [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting) 语法高亮

  ```bash
  git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
  ```

- [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions) 自动补全

  ```bash
  git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
  ```

编辑配置文件

```bash
plugins=(git zsh-syntax-highlighting zsh-autosuggestions)
```

### 增强版 top

```bash
sudo pacman -S htop
```



