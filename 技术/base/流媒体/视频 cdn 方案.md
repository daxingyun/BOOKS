# 视频 cdn 方案
## 方案
- 直播 sdk
	- 推流
		- obs
		- 流视频 (sdk)
		- 几万 sdk
	- 拉流
		- 流播放器(拉流sdk) 

- 流处理
	- 切片
	- 转码
- 播放
	- 拉流
	- cdn
		- 500个点
		- 联通/移动/电信（移动比较多）
		- 湖南省 

- ufile
- 存储视频文件
	- 用来做历史

- 直播存储分片  1-3 分钟 	 

- 延迟比较低
	- 2-6秒之间

- 源-边缘节点同步问题
	- 公网
	- 边缘节点被请求
	- 源站更新

## cdn 分层
- 源站点
	- 公网
	- 1g
- 中间层
	- 公网 
- 边缘节点
	- 公网  	  

延时实测

## 现成直播第三方 demo
- 金山云直播
- 腾讯云直播
- 声网

## 问题
- 视频 1080p

	带宽消耗 8500kp  
- 价格
	- cdn
	
		10 GB 
