# web3.0 开发平台
整体架构设计是走 serverless ，用户只需要编写 js 完成整个 dapp 开发，而不需要关注服务器

为开发者提供开发、测试、生产的整体一体化无缝开发服务体验，从本地链到测试网再到生产网。平台核心会监控链上发生用户的事件同步到用户数据库中，并且可以进一步选择同步监听智能合约的事件，以便用户可以使用传统 web2.0 的数据库访问速度来查询 web3.0 的数据。

整体概念增加 web3 应用用户的用户体验

## 平台做到
- 开发者可以仅使用 js 来开发整个 dapp 服务，而将服务器的所有需求依托于 web3.0 开发平台。
- 同时还支持多链(同 eth 架构)的功能，并且有能力从各种地址获得实时的交易事件，并且还有这些地址所有的历史交易。在数据库使用同一用户体验。
- 还支持去中心化存储功能来处理 dapp 数据
- 所有一些调用尽量贴近只需要一行代码操作，比如对存储的操作就是一行存储和一行代码读取

## 平台不做
- 职能合约需要客户自己去编写(这块主要是公链安全性问题)
- Dapp 前端需要用户自己去处理

## 客户的基础知识
- 对对象、json、mongodb 了解
- 数据库查询的基本知识，限于 mongodb
- javascript 前端和 javascript 云函数 后端了解
	- 理解异步操作
		- Promises,
		- async
		- await
- web3知识
	- 区块链工作原理
	- 原生 web3 api
	- metamask 使用方法，钱包和账户允许交互签名解决方案
	- 熟悉智能合约和合约事件
	- 使用过链进行本地开发
- 软件
	- ide
	- 本地托管1个页面
		- 本地托管环境必须公开托管到平台要求的服务器上
		- 使用 live server 扩展
		- 或使用 pythone 内置服务器
	- git 和代码仓库了解
- 演示可能使用工具
	- nodejs
	- ganache
	- truffle

## 什么是 web3 Dapp
- UI
	- 功能
		- 用户界面  
	- 语言
		- JS
			- web3.js(用来与合约交互)   
- Server 提供业务的同时，还提供调用合约(运行在链上)
	- 功能	 
		- 用户管理
			- 聚合用户数据(链功能)
			- 用户身份验证
			- 用户信息配置
				- 如头像、电子邮件、电话等等
			- 设置用户链事件告警
				- 与用户所有相关链信息的告警 ，比如拥有的 NFT 被交易、token 交易、应用登陆、登陆ip异常等 
		- 过滤器
		- 聚合(链功能)
			- 聚合历史数据(区块链节点没有这个能力)  
	- 语言 
- 智能合约
	- 功能
		- 财务逻辑
			- token 管理
				- 余额 
			- NFT 管理
				- 余额                  
	- 语言
		- solidity
	- 开发辅助工具
		- ganache(本地私链)
			- 加速开发，虽然可以用公网测试链，但是那个会很慢
	- 开发智能合约工具
		- truffle
			- 编译、部署、运行


## 服务端具体接口
- 用户认证与用户管理
	
	提供端到端的 web2和3 的单一用户管理 
	
		moralis.autherticate().then((user) => {
			console.log(user.ethAddress); //获取用户地址
			console.log(user.transactions); //获取交易
			console.log(user.email); // 获取邮箱
			console.log(user.name); // 获取电子邮件
		})
- 实时与数据库链接
	- 允许你存储或同步任何 json 数据 
	- 百万级用户管理能力
- 实时报警
	- 链告警通过 webhook 或 socket
		- 交易
		- 转账
		- 铸造
		- 等
- 服务逻辑(通过云编码)
	- 做任何访问数据库的业务逻辑
	- 与区块链交互，可以读取区块链和智能合约的状态
- 数据存储
	- 存储任何数据
- 支持跨链能力       			


# 平台产品功能
## 用户管理
## 创建服务
- 服务名称
- 选择服务启动的区域(比如香港)
- 服务选择的链网络
	- 公链
	- 测试链
	- 本地链(就是用 ganache 启动一个测试链)

## 服务详情
- 服务器详情
	- 服务名
	- 服务 url
	- 应用id
	- masterkey
	- 仪表盘
		- 用户
		- 密码 
- 本地链 proxy 设置
	- 下载 proxy 程序与应用服务器连接 


	 


## 前端开发
- 主函数
	- 初始化服务(填写服务id)
	- 服务 url (填写服务器的ip地址)    			      
