# 1212
今日学习：一些高数；一道绿题（超时了一个点）；cs61a Coroutines
感想：我们必须提高对自我的掌控力，从中获取满足感（这真的是对的吗？？）
高数仍需加强学习；做题是不是模拟的意思太多了？cs61a得抓紧了！！
明天：暂且无事；能不能约人出去玩？
# 1213
约人出去玩太难了。
早睡早起的核心要点在于早睡。
我们应当 ___崇尚___ 科学的学习方式
我注意到有同学的高数、线代水平已臻化境了。我们是不是应该抓紧了呢？
# 1215
尝试在寝室自习了一天。不好说效率高还是低：或许是我在外自习的效率太低了！
引人思考的一段话。
	多啰嗦两句：我上大学的时候，其实和你们差不多，也不爱上课，上课就是聊天睡觉。要说我和你们有什么区别，就是我在考试前能靠着小聪明拿到一个还可以的分数，其实学的不怎么样。当时心里还很窃喜，现在回想起来，人生的上限就是在不知不觉中逐渐降低的。一晃快20年，到了现在这个岁数，这辈子基本定型。普通人（包括我也是）和精英的差距在哪里？不在于智力，更多在于认知。然而，人的认知极难改变，这也就是为什么绝大多数人的命运出生就已注定。很多东西，你们这个年纪很难理解，20年后，明白了也没什么用了。不过话说回来，人生就这么回事，最终归宿都一样，想开了也没什么。
# 1216
在wsl忙了一天。。。
从git上下文件，还算顺利
先是研究docker，配置了半天，一开始用分发软件的版本，没有dockercompose又忙了好久
dockercompose搞好之后再build，又出问题了：网络不行。换了几个镜像源，都不行，最后让linux能用v2rayn的端口上网了，不知道build能执行不。
<details>  
  <summary>一些问题：</summary>  
```  
git是ubuntu内置的吗
	docker-compose up -d --build 解释各个参数的意义
	[http://localhost:5000](http://localhost:5000/)这个网页是什么
	docker-compose logs -f
	docker-compose down
	docker-compose ps
	真正的 Docker CLI
	sudo usermod -aG docker $USER
	newgrp docker
	sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
	```
ls -lh /etc/apt/keyrings/docker.gpg
```
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
```
sudo systemctl status docker
sudo journalctl -xeu docker
```
什么是Docker daemon 配置文件
为什么**允许局域网连接**后就能在wsl内用vpn？wsl和windows主系统在网络上是什莫关系
 HTTP 代理端口（默认 `10809`）和 SOCKS 端口（默认 `10808`）是啥
 ```
export WINDOWS_IP=$(ip route | grep default | awk '{print $3}')
echo $WINDOWS_IP
```
**TCP**是啥
```
netstat -ano | findstr 10809
```
netsh interface portproxy add v4tov4 listenport=10810 listenaddress=0.0.0.0 connectport=10809 connectaddress=127.0.0.1 啥意思？有啥影响？如何取消？
  TCP    127.0.0.1:10809        0.0.0.0:0              LISTENING       20032
  TCP    127.0.0.1:10809        127.0.0.1:49901        ESTABLISHED     20032
  TCP    127.0.0.1:10809        127.0.0.1:54963        TIME_WAIT       0  都是啥意思？
```  
</details>
# 1217
考试。5h 3题，燃尽了。有几道题感觉能做但是就是过不了。acm赛制给的提示很少，吃一发WA对解题没啥帮助。明天把几道开了没做出来的题看一下，一定要把英语作文写了！
口琴、语言的良好习 惯不能丢。高数线代再不复习就积重难返了。

# 1224
英语口语在湖边练习，很清静。

# 1226
疯狂的一天！5点出去玩->11：30结束->地铁停运->骑自行车回学校->宿舍锁门->图书馆过夜->早7点起床

# 228
程序员（也许ai？）比任何人想象的都要容易犯错。如何纠错？interface -> __test__  -> implement 

# 309
从做题到做项目，这些事无不给我一个启示：每时每刻管理复杂性
什么是复杂性？从算法题各个变量，逻辑的综合，到项目的类接口，函数接口
人脑绝对不能记忆过多的信息，难以完成太复杂的项目
如何改进？函数式编程？常用抽象？详实记录接口的注释？


## 415
但问耕耘莫问收获是完全错误的：带来的是完全的效率低下
需要一个TODOLIST软件：长期任务（每周干什么）+短期目标（明天干什么）+备忘录（对任务拆解）用任务倒逼效率。例如，我要在接下来两个小时内搞定bomblab phase2
