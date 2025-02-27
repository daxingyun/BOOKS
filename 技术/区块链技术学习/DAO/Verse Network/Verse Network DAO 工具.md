# Verse Network DAO 工具
## 需求
时间|名称|目的|筹款金额
---|---|---|---
2022|AssangeDAO|解救维基解密创始人阿桑奇|1.74万枚ETH
2021年11月| ConstitutionDAO|众筹拍卖美国宪法副本|1.16万枚ETH
-|FreeRossDAO|解救暗网市场“丝绸之路”|-
-|Krause House DAO|收购NBA球队|-
-|BlockbusterDAO|计划收购倒闭的电影租赁公司Blockbuster|- 

## 痛点问题
- 技术问题
	
	加密行业智能合约开发难度大，加上项目开发还涉及前端、后端等编程技术，对普通用户而言，自己创建一个DAO的门槛较高；
- 市场问题
	- 市场上新DAO项目推出速度快，用户难以即时获取相关信息以及成为早期社区成员；
	- 当用户参与的DAO较多时，难以便捷地进行统一管理；
- 费用问题
	- 目前绝大多数DAO项目发行在以太坊上，Gas费较高，且DAO投票和治理方法复杂，对普通用户要求较高。

### STP Network 宣布推出 Verse Network
#### 目的
一条专门为优化DAO而构建的 Layer 2 侧链，旨在为下一代 DAO 和 DeFi 协议提供抗审查、抗抢先交易以及高性能的技术方案。
#### 技术
Verse Networ 由 STP Network 和 Meter Foundation 共同开发，建立在基于 HotStuff 共识的 Meter SDK 框架上

- 可扩展到 1000 个验证节点，具有高度的可扩展性
- 较高的TPS（每秒处理的交易数），约为1500
- 支持多个虚拟机，如 EVM、WASM 和 MOVE，可与以太坊、波卡、BSC等区块链网络互连互通。
- 低Gas费，大约为0.05美元~0.5美元
- 抗抢先交易，所有用户均不能通过支付更高 Gas 费使其交易提前获得批准和验证

### Dapp 产品
- Framework

	是一个支持用户创建DAO的工具，使任何用户均可轻松创建自己的DAO，根据PANews的亲身体验，几分钟即可完成。
- Clique
	- Clique 是一个可视化 DAO 管理仪表板，使用户轻松查看自己在 Verse Network 上所有的 DAO 和资产，便于统一管理，如参与不同 DAO 的投票、发起 DAO 的提案等。
	- 此外，Clique 还为用户提供 Verse Network 上发布的其它 DAO 的信息，便于用户即时参与代币发售活动。

### 操作步骤
#### [Framework](https://daoframe.com/#/) 支持 rinkeby
- 创建 DAO 主页
	
	![](./pic/1.png)
	
	- 分新建代币创建 DAO
	- 使用当前代币创建 DAO
- 使用以有代币创建 DAO
	
	![](./pic/1-1.png)
	
	- 当前链已有 ERC20 合约创建

		![](./pic/1-2.png)
	
		- DAO 名称
		- 代币合约地址
		- 描述
		- 官方网站
		- 代币图片
		- 社交媒体链接（如Twitter、Discord）
	- 跨链治理(支持 verse 和 polygon) 
		 - ![](./pic/1-3.png)
		 
		暂时不可用
- 分新建代币创建 DAO
	- 基础信息设置
	
		![](./pic/2.png)
		
		- DAO 名称
		- 代币名称
		- 代币最大供应量
		- 代币精度
		- 代币代称
		- 官方网站
		- 代币图片
		- 社交媒体链接（如Twitter、Discord）
	-  Token 分配机制
	
		![](./pic/3.png) 
		
		- 预留代币的地址
		- 相应解锁时间
		- 用户可选择
			- 否进行白名单发售
			- 公开发售
			- 起始时间
			- 终止时间
		- 白名单和公开销售
			
			 ![](./pic/4.png) 
			
			- 白名单地址是谁可以买多少价格是多少
			- 兑换 DAO 代币的价格（需指定用什么代币来兑换，目前默认为测试代币）
			- 公售中每个用户最小/大购买量等信息
	
			如果不需要白名单才可以买，直接公开发售即可
			
			 ![](./pic/4-1.png) 
	- 投票规则
		
		 ![](./pic/5.png) 
		
		- 参与投票的最低代币持有量
		- 创建提案的最低代币持有量
		- 投票有效的最低参与率（使投票结果有效所需的最低代币数）
		- 社区提案投票时长(可选择由提案人自定义，但最低设置3天)
		- 合约提案投票时长
		- 等
	- Review
		- ![](./pic/6.png) 
		- ![](./pic/6-1.png) 
		- ![](./pic/6-2.png) 
	- 确认
		- ![](./pic/6-3.png) 
		- ![](./pic/6-4.png)
		- ![](./pic/6-5.png) 
		- ![](./pic/6-6.png) 
			
#### [Clique](https://test.myclique.io/) 支持 rinkeby
Clique 主要提供两大功能
	
- 允许用户参与 Verse Network 上其它 DAO 代币的发售活动；
- 使用户在单个仪表盘中管理自己所有的DAO，如发起提案、参与投票等。
	
#####  首页预览
首页分成3个部分，页眉、工具栏、主功能页
	
![](./pic/7.png) 
	
- 页眉

	除了我的钱包意外，其他功能同登陆功能
	
	![](./pic/7-0.png) 
	
	- 钱包功能
		- 钱包 

			这里可以查看到以太坊剩余，但是无法查询到 DAO 名称，可能是我当前没有持有任何 DAO token
			
			![](./pic/7-1.png) 
		- 历史

			当前空
			
			![](./pic/7-2.png) 
	- 点击 Clique 图标返回首页			
- 工具栏	页面(左侧)
	
	可以看到自己 DAO 按钮和一个添加新 DAO 按钮
	
	-  自己 DAO 按钮

		点击进入自己的 DAO 页面
		
		![](./pic/7-3.png)
	- 添加一个新 DAO 按钮		
		- 按下跳转 [Framework](https://daoframe.com/#/create) 产品页面-老版本
		- 新版本直接跳转创建页面(感觉就是合并了 Framework 功能)
- 主功能页面
	
	主功能区也有两个部分
	
	- 按钮区
		
		包含两个功能按钮， DAO 按钮和公开发售按钮
	- DAO 功能区
		- DAO 按钮显示的功能区
		
			注意默认使用 DAO 按钮展示的功能区，可以看到
			
			- 建立的 DAO，包含自己和其他人
			- 目前的成员数
			- 提案数量
			
			![](./pic/7-4.png)	
		- 公开发售按钮显示的功能区

			可以看到
	
			- 所有已经建立的 DAO(包含自己和其他人)
			- 模式
				- 公开发售
				- 白名单发售
				- 私有发售
			- 项目进展
				- 开启
				- 关闭
				- 准备发售
			- 已出售发行进度条  
			- 发行量
			- 发行比率
			- 发售时间
			- 等信息

#### 项目购买页面
在主功能页面，选择公开发售按钮后，就切换到了发售项目页面。

可以点击没有售完的 Acitve 项目，分3个部分
	
- 项目基本信息
	- 项目名
	- 查询项目详情按钮(跳转项目详情页，并非游览器跳转) 
	- 出售金额
	- 出售金额进度条
	- 成员数量
	- 关闭时间
	- 功能按钮
		- 关于

			显示项目的描述信息
		- 活动 

			显示购买信息和领取信息
			
			- 购买信息

				购买后没有马上显示，这可能是跟同步显示有关
				
				可显示购买交易相关数据
				
				- 交易金额描述(比如什么Token 购买了 DAO Token)
				- 交易时间
				- 交易TXID(可以点击跳转游览器)
				
				![](./pic/13.png)
				
			- 领取信息

				可以显示领取的
				
				- 交易时间
				- 交易TXID(可以点击跳转游览器)
				- 金额
				
				![](./pic/14.png)
- 公开发售信息
	- 资金目标
	- 兑换汇率
	- 兑换可填写数量范围
	- 置换 DAO Token 数量(手动填写)
	- 支付 Token 数量 (自动转换)
	- 支付 Token 余额显示 (自动获取)
	- 可以置换限额(每地址限额)
	- 支付文字提示
	- 支付按钮

	参与参与购买
	
	- 输入置换 DAO Token 数量(数量限制在上面的范围)
	- 点击支付
		- ![](./pic/10.png)
	- 购买成功
		- ![](./pic/11.png)	
	- 购买页面刷新

		可以显示
		
		- 销售进度
		- 成员
		
		![](./pic/12.png)			 
- 保留 Token

	之前建立项目预分配的额度在这里申请，包含
	
	- 保留额度
	- 锁定期(过了才能领不过不能领)
	- 宣领按钮
		- ![](./pic/8.png)
	
	点击声明领取(这个按钮做这里很怪)
	
	- 声明只能做一次，做完不可以在点击，且除了打开了投票按钮，其他没有任何显示
		- ![](./pic/9.png)
	
	购买完毕后返回首页
	
	![](./pic/15.png)

#### DAO 项目治理
在主功能页面，选择 DAO 按钮后，就切换到了治理项目页面。

- 暂时没有参与项目的登陆情况
	- ![](./pic/16.png)
- 参与项目的登陆情况
	- ![](./pic/17.png)	
	
点击自己占有份额的项目，也可以在左工具栏选择自己参与的项目。

就可以对项目进行根据份额相关的治理，分4个功能页：提案、资产、成员、项目配置

- 项目治理配置

	![](./pic/18.png)
	
	- 合约信息
		- 治理合约地址
		- Token 合约地址
	- 保留额度地址
		- 编号
		- 地址
		- 额度
		- 项目占用百分比
		- 锁定期
		- 总供应量
	- 治理配置(等同于创建设置)
		- 修改前
			- ![](./pic/19.png)
		- 修改设置
			- ![](./pic/20.png)
		- 修改提案
			- ![](./pic/21.png)
			- ![](./pic/22.png) 		
- 提案

	点击提案，可以看到提案 
	
	![](./pic/23.png) 	
	
	- 创建提案

		创建提案除了可以和上面的方式通过修改治理合约规则外，还可以通过提交按钮直接提交一般提案
		
		![](./pic/24.png) 	
		
		- 编辑提案配置
			- ![](./pic/25.png) 
		- 质押提交
			- ![](./pic/26.png) 
			- ![](./pic/27.png) 	
			- ![](./pic/28.png)
		- 查看投票项目 
			- ![](./pic/29.png)
	- 撤销提案
		- 点击刚才建立的提案进入投票页面，可以查看
			- 提案介绍
				- 启动时间
				- 结束时间
				- 提案名称
				- 提案介绍
				- 提案状态
					- 启动
					- 关闭
					- 结束
						- 失败
						- 成功    
			- 投票结果
				- 赞成
				- 反对
				- 其他
				- 查看投票详情按钮
					- 投票详情列表
						- 用户
						- 选择投票方
						- 投票数额  
			- 用户投票操作界面
				- 单选操作
					- 赞成
					- 反对
					- 其他
				- 用户
					- 可投票金额
					- 最小投票金额       
			- 提案历史时间
				- 事件类型
					- 创建(链交易可使用游览器查询)
					- 激活
					- 取消(链交易可使用游览器查询)
			- 详细信息
				- 初始化用户(创建提案的用户)
				- Snapshot ID
				- 启动时间
				- 结束时间
				- staked
				          
			 ![](./pic/30.png)
		- 点击撤销提案并认领资产
			- ![](./pic/31.png)
		- 链同步确认
			- ![](./pic/32.png)
		- 点击进入查看
			- ![](./pic/33.png)
		- 注意撤销提案可以回收提案抵押 DAO Token
	- 投票提案通过
		- 按照创建提案再创建一个新提案
	
			![](./pic/34.png)
		- 进入提案投票
			- 投通过票数
				- ![](./pic/35.png)
				- ![](./pic/36.png)
				- ![](./pic/37.png)
				- ![](./pic/38.png)
			- 投反对票数
				- 切换账户，同上原理
			- 投票当前情况
				- ![](./pic/39.png)
			- 等待结束
			- 投票结束
				- ![](./pic/40.png)
			- 非创建提案的人查看
				- ![](./pic/41.png)
			- 创建提案的人查看(注意这里提案人可以取回提案抵押)
				- ![](./pic/42.png)
	- 投票提案失败
		-  按照通过设立相反的投票
		-  投票结果
			- ![](./pic/43.png)
		- 非创建提案的人查看
			- ![](./pic/44.png)
		- 创建提案人查看
			- ![](./pic/45.png) 
	
		![](./pic/46.png) 	
- 成员

	查看持有 DAO Token 地址的各种信息，包括
	
	- 成员总数
	- 排行
	- 地址
	- Token 数量
	- 比例
	- 提案数量	

	![](./pic/47.png) 
- 资产
	- 主控制页
	
		切换到资产页面，可以查看到
		
		![](./pic/48.png) 
		
		- DAO Token 储备
			- DAO Token
			- ETH Token
			- 其他 Token 
		- 存款/提款账单
			- 操作(存/取)
			- Token 名称
			- 时间
			- 数量
			- 交易 TXID 游览器转移按钮
		- 操作按钮
			- 存款
			- 取款
	- 存款过程
		- 界面
			- 资产名选择菜单
				- DAO Token
				- ETH Token
				- 其他 Token
			- 账户当前余额
			- 存款数量
			
			- ![](./pic/49.png)
		- 存款交易 
			- ![](./pic/50.png)
		- 交易结果
			- ![](./pic/51.png)
	- 取款提案过程

		取款和存款不同，需要投票决定是否可取
		
		- 取款提案界面
			- 资产名选择菜单
				- DAO Token
				- ETH Token
				- 其他 Token
			- DAO 对应选择资产名的余额
			- 取款数量
			- 取款说明
			- 当前用户余额
			- 创建提案需要的质押金
			- 创建提案按钮

			![](./pic/52.png)
		- 取款提案确认界面
			 - 提案名称
			 - 提案启动时间
			 - 结束时间
			 - 质押数额 
		
			![](./pic/53.png)
		- 查看提案

			![](./pic/54.png)

## 测试
### 治理测试
- 已知
	- 用户 A 有 400 DAO Token
	- 用户 B 有 200 DAO Token
	- 每建一个提案需要 100 DAO Token
- 测试 A

	双投票测试 ERC20 限额(同时多个提案)
	
	- 测试目的
		- 验证限额逻辑
		- 验证扣费逻辑
		- 验证投票逻辑
	- 测试开始
		- 用户 A 测试创建2个不同提案，各扣费 100 DAO Token
		- 提案建立好后，用户 A 在2个不同的提案分别投票
	- 测试结果
		- 投票的时候 DAO Token 只有 200，但是投票可以按照 400 进行投票
		- 单个提案投票只能投出所有票数，而金额不是200 而是 400
	- 结论
		- DAO  Token 仅限制创建提案的数量，不限制投票数量
		- 投票分别计票，没有在 A 提案投票， B 提案就无法投票
		- 普通投票仅仅只有投票，没有和合约操作做关联      

## 问题
- 一个用户可以同时创建2个提案，2个提案？都能投全票？如何实现
- 投票提案使用的是 ERC20 限额度，而没有使用转账，这个是为了节省 gas 费？
	- 限额只有全部限额和不限额，所以只能全部？	    
			   
## 参考
- [零基础也能玩转DAO，Verse Network如何让DAO零门槛](https://m.thepaper.cn/baijiahao_16710485)
- [verse-network](https://stp-dao.gitbook.io/verse-network/verse-network/master)	
	
	
	

		
	

		
	
			  
	

	
	




	