# NDock 基本介绍

> __Keywords__: NDock, 介绍

NDock 是一个服务器应用容器, 他能用宿主和管理你的多个后端服务。


## 程序集介绍

* NDock.Base.dll： 		NDock 基础共享程序集, 你的NDock容器服务和NDock应用程序(NDock App)需要引用它;
* NDock.Server.exe: 	NDock 容器服务. 它能以控制台程序和Windows服务的形式运行;
* NDock.Worker.exe:		NDock worker. 如果NDock以Process的隔离模式运行, NDock worker 将会以载体进程的形式运行你的 NDock App.


## 定义你的 NDock App

基于 NDock AppServer 基类定义一个类, 然后实现需要的方法。
并且给该类添加 attribute AppServerMetadata 用于定义其唯一名称。这个唯一名称将会用于 NDock 配置之中.

	using System;
	using System.Configuration;
	using NDock.Base;
	using NDock.Base.Config;
	using NDock.Base.Metadata;
	
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

下面的xml文件是一个完整的NDock配置示例:

	*	NDock.Server.exe.config
	
	<?xml version="1.0" encoding="utf-8" ?>
	<configuration>
	  <configSections>
		<section name="ndock" type="NDock.Base.Configuration.NDockConfigSection, NDock.Base"/>
	  </configSections>
	  <appSettings>
		<add key="ServiceName" value="NDockService"/>
	  </appSettings>
	  <ndock>
		<servers>
		  <server name="TestApp"
				  type="TestAppServer">
		  </server>
		</servers>
	  </ndock>
	</configuration>
	

#### 在appSettings配置节的属性 "ServiceName" 定义了NDock以服务形式运行时的 windows service 名称。:

	<add key="ServiceName" value="NDockService"/>

	
#### 下面的配置意味着这个 NDock 服务器定义了一个名为"TestApp"的 NDock app，它的类型名称为"TestAppServer"。 该类型 定义在你的 NDock AppServer 类的 attribute AppServerMetadata中:

	<servers>
	  <server name="TestApp"
			  type="TestAppServer">
	  </server>
	</servers>
	
## 运行 NDock

NDock的入口可执行文件为 "NDock.Server.exe"。 你可以双击运行它， 然后程序会询问你是否要直接运行它还是安装其为 Windows 服务。

NDock.Server.exe 也可以接受额外的参数:


### 以控制台形式直接运行:

	NDock.Server.exe -c


### 安装其为 Windows 服务:

	NDock.Server.exe -i

	
### 卸载之前安装的 Windows 服务:

	NDock.Server.exe -u

	