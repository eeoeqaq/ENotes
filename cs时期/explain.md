
	Go核心概念 
	   语法： range for 
		“_”开头的标识符忽略unused 
		标识符开头大小写决定公开性 
		:=声明新变量，var声明未初始化的新变量
		 nil相关类型（均为指针或肥指针类型）
		if xxx := yyy; xxx {}声明并判断（语法糖） 
		函数的多返回值与Go习惯的编程范式 
		 struct与关联函数 
		 goroutine、chan与select多路复用 
		 可变参数包（可跳过） 
		interface与decktype隐式实现，interface类型的底层是指针 
		  any（或interface{}）类型擦除，以及恢复时的类型断言 
		  struct与function泛型 
		  type定义别名、新类型、struct、interface 
		  struct的embedded struct（组合优于继承的语法糖），interface的composition
		   GC与变量逃逸（可跳过） 
		   结构体字段tag与JSON序列化反序列化 
	   标准库： 
	    fmt格式化库 slog日志库（→zap日志库） errors错误库 os操作系统库 io输入输出辅助库 sync并发原语库 time时间库 encoding/json序列化库 
		   三方库：
		 HTTP框架：Iris v12 
		 ORM：GORM 
		 日志库：zap 
		 JWT：jwt 
	   设计模式与编程范式：
	    guard clause与early return 
	    函数式编程 
	    依赖注入 
	    HTTP服务器基本三层架构
	    基于context的超时取消 
	    RESTful API（简单看看，不一定用） 
	    结构化日志 
	    其他： 
		集成测试与单元测试 
		静态检查与风格检查

protocol buffer
gRPC
	https://info.support.huawei.com/info-finder/encyclopedia/zh/gRPC.html
zap 
feed：前端给后端发送请求；后端给出一个list，用于前端的scroll缩略图构建
			![[Pasted image 20260330134050.png]]