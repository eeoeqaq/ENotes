下载合适版本的java，配置jenkins下载路径，下载
```bash
sudo apt install fontconfig openjdk-21-jre
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
https://pkg.jenkins.io/debian-stable binary/ \
| sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update
sudo apt install jenkins
```
设置端口为8080
```bash
sudo systemctl start jenkins
sudo systemctl status jenkins #检查是否启动
```
###### SSH尝试
公钥上传至gitlab（发现我已经上传过了，不好的预感）
私钥直接粘贴给jenkins，连接显示 `Connection closed by 115.156.123.33 port 22`
nmap能扫到22端口，但` ssh -T -i ~/.ssh/id_ed25519 git@csgitlab.whu.edu.cn`不给进
转战http   和HTTP git remote一样的流程
构建阶段，用仓库名和配置的access密钥pull仓库main分支内容，在本地构建/测试
###### 新问题
构建失败：无法从github上下载依赖包
`crul -I https://www.google.com`可以
`crul -I https://www.github.com`不行
百思不得其解，修了半天重启了wsl，这下jenkins都打不开了

day2：解决了，换了一个梯子节点。

新问题：git fetch 超时，应该是jenkins用户的问题。以下是claude生成的错误解析

`sudo ip link set dev eth0 mtu 1500`
## 问题最终确诊

**根因：WSL2 网络接口 `eth0` 的 MTU 被设置为 9000（Jumbo Frame），但网络路径中某个环节（校园网出口/中间路由设备）只支持标准 1500 MTU，且该设备的 ICMP "需要分片"通知被防火墙拦截，导致经典的 PMTU 黑洞（Path MTU Discovery Blackhole）。**

表现为：

- 小数据包（TCP 握手、HTTP 请求头）能正常通过 → 连接看起来"建立成功"
- 一旦需要传输较大数据（GitLab 认证响应、fetch 的 pack 数据）→ 大包被中间设备静默丢弃，且不返回任何拒绝或错误信号
- 本地这端只能傻等，永远等不到响应，表现为"卡死不动"而非报错

## 解决方法

```bash
sudo ip link set dev eth0 mtu 1500
```

把 MTU 从 9000 降到标准的 1500，绕开中间设备无法处理巨型帧的问题。

## 排查过程回顾（走过的方向）

| 排查方向                              | 结果                                                                                          |
| --------------------------------- | ------------------------------------------------------------------------------------------- |
| Jenkinsfile / vcpkg 下载 zlib 失败    | 发现根因是访问 GitHub 网络受限，属于表层现象                                                                  |
| JUnit 报告误抓 `.clang-format`        | 修正了 fileset pattern，解决了次要问题                                                                 |
| curl 测 google.com 通、github.com 不通 | 引出网络层面排查方向                                                                                  |
| WSL 连接 Windows 本机代理               | 确认走镜像网络模式，找到正确代理地址 `127.0.0.1:10808`                                                        |
| GitHub 返回 403 Access Restricted   | 确认是代理节点信誉问题，与本次 GitLab 问题是两条独立线索                                                            |
| git fetch 卡住疑似分支名错误               | 排除，fetch 命令本身抓取所有分支，与分支名无关                                                                  |
| Jenkins/脚本全局代理配置                  | 检查、清空，问题依旧存在，排除                                                                             |
| 仓库级 `.git/config` 代理残留            | 检查为空，排除                                                                                     |
| `.git` 目录锁文件、文件权限混乱               | 检查无异常，排除                                                                                    |
| Token（PAT）替代密码认证                  | 排除凭证失效问题，但仍卡死，说明不是认证方式问题                                                                    |
| **`strace` 追踪卡住的进程**              | **决定性线索**：发现卡在 `poll()`／`pselect6()` 等待 socket 数据，且 TCP 连接状态是 `ESTABLISHED`——说明连接建立成功但数据收不到 |
| 怀疑 Docker 网络 NAT                  | 排除，未安装 Docker                                                                               |
| WSL 自动代理变量（`http_proxy` 等）        | 确认存在，但与 jenkins 直连 GitLab 80 端口的黑洞是两个独立问题                                                   |
| **检查网卡 MTU（`ip addr show`）**      | **发现 `eth0` MTU=9000**，此前用 1500 标准值做的 MTU 测试（`ping -s 1472`）因为远小于 9000，未能触发真正的临界问题，是一次"假阴性" |
| **降低 MTU 至 1500**                 | **✅ 问题解决**                                                                                  |

## 关键教训

`strace` 精确定位到"卡在等 socket 数据"而非"等锁"或"等终端输入"，是这次排查的转折点；而**第一轮 MTU 测试之所以给出误导性结论（"MTU 没问题"），是因为测试时假设了错误的基准 MTU（1500），而实际网卡是 9000**——这提醒我们，做 MTU/PMTU 黑洞排查时，一定要先确认实际网卡 MTU，再据此计算测试用的包大小，而不是想当然套用标准值。

持久化解决：
`sudo systemctl edit jenkins`
在其中加入
`[Service] 
`ExecStartPre=/usr/sbin/ip link set dev eth0 mtu 1500`
