## 使用 SSR 代理

### 1 客户端的安装

采用 Qv2ray 客户端，通过安装插件支持SSR订阅

Qv2ray：https://github.com/Qv2ray/Qv2ray

SSR 插件：https://github.com/Qv2ray/QvPlugin-SSR

官方教程：https://qv2ray.net/getting-started/

安装：

```bash
pacman -Sy v2ray qv2ray # 核心和前端
sudo pacman -S qv2ray-plugin-ssr-dev-git # ssr支持插件
```

添加订阅：分组 - 添加订阅 - 订阅设置 - 勾选此分组是一个订阅 - 粘贴链接 - 更新订阅 - 确定

### 2 浏览器代理设置

配置 Proxy SwitchyOmega 代理插件

### 3 git 代理设置

.gitconfig 中写入如下内容：

```bash
[http]
        proxy = http://127.0.0.1:8889
[https]
    	proxy = http://127.0.0.1:8889
```

或者通过命令：

```bash
# 配置代理
git config --global http.proxy http://127.0.0.1:1080
git config --global https.proxy http://127.0.0.1:1080
# 取消代理
git config --global --unset http.proxy
git config --global --unset https.proxy
```

### 4 终端 curl 和 wget 代理设置

终端 curl 和 wget 等都会使用`<PROTOCOL>_PROXY`环境变量提供的代理，因此只需要添加如下环境变量：

```bash
export http_proxy="http://127.0.0.1:8889"
export https_proxy="http://127.0.0.1:8889"
```

