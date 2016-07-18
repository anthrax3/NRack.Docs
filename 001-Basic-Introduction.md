# NRack 基本介绍

> __Keywords__: NRack, 介绍

NRack 是一个服务器应用容器, 他能用宿主和管理你的多个后端服务。


## 程序集介绍

* NRack.Base.dll： 	 NRack 基础共享程序集, 你的NRack容器服务和NRack应用程序(NRack App)需要引用它;
* NRack.Server.exe: 	NRack 容器服务. 它能以控制台程序和Windows服务的形式运行;
* NRack.Worker.exe:		NRack worker. 如果NRack以Process的隔离模式运行, NRack worker 将会以载体进程的形式运行你的 NRack App.


## 定义你的 NRack App

基于 NRack AppServer 基类定义一个类, 然后实现需要的方法。
并且给该类添加 attribute AppServerMetadata 用于定义其唯一名称。这个唯一名称将会用于 NRack 配置之中.

	using System;
	using System.Configuration;
	using NRack.Base;
	using NRack.Base.Config;
	using NRack.Base.Metadata;
	
	[AppServerMetadata("TestAppServer")]
	public class TestAppServer : AppServer
  {
		public override bool Start()
		{            
				// the start code	
				return true;
		}

		public override void Stop()
		{
				// the stop code	
		}
}


## 基本配置

下面的xml文件是一个完整的NRack配置示例:

	*	NRack.Server.exe.config
	
	<?xml version="1.0" encoding="utf-8" ?>
	<configuration>
	  <configSections>
		<section name="NRack" type="NRack.Base.Configuration.NRackConfigSection, NRack.Base"/>
	  </configSections>
	  <appSettings>
		<add key="ServiceName" value="NRackService"/>
	  </appSettings>
	  <NRack>
		<servers>
		  <server name="TestApp"
				  type="TestAppServer">
		  </server>
		</servers>
	  </NRack>
	</configuration>
	

#### 在appSettings配置节的属性 "ServiceName" 定义了NRack以服务形式运行时的 windows service 名称。:

	<add key="ServiceName" value="NRackService"/>

	
#### 下面的配置意味着这个 NRack 服务器定义了一个名为"TestApp"的 NRack app，它的类型名称为"TestAppServer"。 该类型 定义在你的 NRack AppServer 类的 attribute AppServerMetadata中:

	<servers>
	  <server name="TestApp"
			  type="TestAppServer">
	  </server>
	</servers>
	
## 运行 NRack

NRack的入口可执行文件为 "NRack.Server.exe"。 你可以双击运行它， 然后程序会询问你是否要直接运行它还是安装其为 Windows 服务。

NRack.Server.exe 也可以接受额外的参数:


### 以控制台形式直接运行:

	NRack.Server.exe -c


### 安装其为 Windows 服务:

	NRack.Server.exe -i

	
### 卸载之前安装的 Windows 服务:

	NRack.Server.exe -u

	