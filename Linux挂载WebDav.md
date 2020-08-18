# Linux 挂载坚果云 WebDav

#### 1 安装 davfs2

```bash
sudo pacman -S davfs2
```

#### 2 挂载

```bash
mkdir ~/jianguoyun
sudo mount -t davfs -o rw,uid=bully,gid=bully https://dav.jianguoyun.com/dav/ ~/jianguoyun
```

报错`/sbin/mount.davfs: mounting failed; the server does not support WebDAV`

修改配置文件

```bash
# /etc/davfs2/davfs2.conf
ignore_dav_header 去掉注释并改为 1
```

#### 3 自动挂载

修改配置文件

```bash
# /etc/davfs2/davfs2.conf
use_locks 去掉注释并改为 0
```

添加用户名密码

```bash
# /etc/davfs2/secrets 末尾添加
https://dav.jianguoyun.com/dav/	用户名	密码
```

之后执行命令便可以挂载而不需要输入密码

```bash
sudo mount -t davfs 					\
	-o rw,uid=bully,gid=bully 			\
	https://dav.jianguoyun.com/dav/ 	\
    /home/bully/jianguoyun
```

可以将上述命令用别名存在 .zshrc 中方便使用

```bash
alias jianguoyun="sudo mount -t davfs -o rw,uid=bully,gid=bully https://dav.jianguoyun.com/dav/ /home/bully/jianguoyun"
```



