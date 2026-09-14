项目初始配置：clang-format代码风格/
day3:
初版MVP：llm agent模块 工具调用模块 权限模块 日志、配置与 CLI 展示模块
跑通初版实现
day4：
进入v2.0 v2.1
添加一个schema步骤：将json格式化的输出请求交给LLM，同时对LLM的回答进行依据于json格式指示文件的检查，若不通过则进一步指示LLM进行修改
所有四个模块：
上下文管理 
日志回放与审计事件
工具安全与 ToolSpec Schema 
自定义指令与多模型 Provider
TODO:README
day5：
实施顺序
1. Skill（已完成）
2. McpTransport + 本地 stdio discovery/call（已完成）
	- 本地MCP stdio + cpp原生工具调用
3. web_search provider + web_fetch 安全客户端 （已完成）
	- (tavily支持)
	- 安全检查
4. Streamable HTTP MCP、认证与会话支持
	- 对其他联网MCP的支持
