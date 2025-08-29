# Install
## 安装旧版本
~~~
bash <(curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh) --version v4.34.0
~~~

## 修改启动配置
1. 修改 v2ray.service 配置 

`vim /etc/systemd/system/v2ray.service`

2. 替换对应配置

`ExecStart=/usr/bin/env v2ray.vmess.aead.forced=false /usr/bin/v2ray/v2ray -config /etc/v2ray/config.json`

3. 重启服务

`systemctl daemon-reload`
## 测试配置可用

`/usr/local/bin/v2ray test -config /usr/local/etc/v2ray/config.json`

## 查看日志命令
~~~
v2ray log
journalctl -u v2ray
journalctl -u v2ray |tail -n 50
~~~

# 锁定配置文件只读，不要乱改了。

`chattr +i example.txt`

# 常用命令

- 查看服务状态

`systemctl status v2ray`

- 重启服务

`systemctl restart v2ray`

- 停止服务

`systemctl stop v2ray`
- 启动服务

`systemctl start v2ray`
