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
export http_proxy="http://${WIN_IP}:10808"
export https_proxy="http://${WIN_IP}:10808"
export all_proxy="socks5://${WIN_IP}:10808"
```
docker build . 时使用如下选项：
```
docker build \
  --build-arg http_proxy="http://$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}'):10811" \
  --build-arg https_proxy="http://$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}'):10811" \
  -t your-image-name . 
```

2026/6/26
https://gemini.google.com/app/8476876328781ff0
上述方法失败了，，采用新方法
### TUN模式
TUN 模式（虚拟网卡模式）是 **Clash Verge** 这类代理客户端中一个非常强大的功能，它能创建一个**虚拟网卡**，从而可以接管设备的所有网络流量……
[TUN模式](https://zhida.zhihu.com/search?content_id=249803514&content_type=Article&match_order=1&q=TUN%E6%A8%A1%E5%BC%8F&zhida_source=entity)是一种网络隧道技术，主要用于VPN（[虚拟专用网络](https://zhida.zhihu.com/search?content_id=249803514&content_type=Article&match_order=1&q=%E8%99%9A%E6%8B%9F%E4%B8%93%E7%94%A8%E7%BD%91%E7%BB%9C&zhida_source=entity)）中的数据包传输。TUN（网络层隧道）和TAP（[数据链路层](https://zhida.zhihu.com/search?content_id=249803514&content_type=Article&match_order=1&q=%E6%95%B0%E6%8D%AE%E9%93%BE%E8%B7%AF%E5%B1%82&zhida_source=entity)隧道）是两种主要的隧道模式，它们在数据包的传输层次上有所不同。TUN模式专注于[IP数据包](https://zhida.zhihu.com/search?content_id=249803514&content_type=Article&match_order=1&q=IP%E6%95%B0%E6%8D%AE%E5%8C%85&zhida_source=entity)（第三层）的隧道化，而[TAP模式](https://zhida.zhihu.com/search?content_id=249803514&content_type=Article&match_order=1&q=TAP%E6%A8%A1%E5%BC%8F&zhida_source=entity)则是处理二层的数据帧。了解TUN模式的优缺点可以帮助更好地配置VPN和网络隧道策略……