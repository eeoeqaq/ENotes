2026/1/20
		https://github.com/copilot/c/3999c5d6-caa5-47d9-b1c0-7f84d8e3fd07
## 1.情况
```
eeoe@eeoeQAQ:~/proj-explain$ curl -I https://www.google.com --max-time 5
curl: (28) Connection timed out after 5012 milliseconds

eeoe@eeoeQAQ:~/proj-explain$ ip route
default via 172.21.128.1 dev eth0 proto kernel
172.17.0.0/16 dev docker0 proto kernel scope link src 172.17.0.1 linkdown
172.18.0.0/16 dev br-f55211efa1b1 proto kernel scope link src 172.18.0.1
172.21.128.0/20 dev eth0 proto kernel scope link src 172.21.139.81

PS C:\windows\system32> netsh interface portproxy show all

侦听 ipv4:                 连接到 ipv4:

地址            端口        地址            端口
--------------- ----------  --------------- ----------
0.0.0.0         10810       127.0.0.1       10809

```

### 2.解决
在~/.bashrc 文件末尾添加了如下内容：

```
# WSL 使用 Windows 代理配置
export WIN_IP=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}')
export http_proxy="http://${WIN_IP}:10811"
export https_proxy="http://${WIN_IP}:10811"
export all_proxy="socks5://${WIN_IP}:10810"
```
docker build . 时使用如下选项：
```
docker build \
  --build-arg http_proxy="http://$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}'):10811" \
  --build-arg https_proxy="http://$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}'):10811" \
  -t your-image-name . 
```