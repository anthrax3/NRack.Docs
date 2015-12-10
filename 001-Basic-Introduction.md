# NDock Basic Introduction

> __Keywords__: NDock, Introduction

NDock is a server application container, which can be used for your back end services' hosting and management.


## Assemblies Introduction

* NDock.Base.dll： 		NDock basic common assembly, which is referenced by NDock container server and NDock application (NDock App);
* NDock.Server.exe: 	NDock container server. It can run as windows service or console application;
* NDock.Worker.exe:		NDock worker. If NDock's isolation mode is Process, NDock worker will work as carrier process for NDock App.


## Basic Configuration

The xml file below is a full NDock configuration sample:

NDock.Server.exe.config	
	
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
	

### The attribute value of "ServiceName" in the appSettings section defines the windows service name if the NDock server runs as Windows Service:

	<add key="ServiceName" value="NDockService"/>

	
### The configuration below means the NDock server has one NDock app defined whose name is "TestApp" and it's type name is "TestAppServer":

	<servers>
	  <server name="TestApp"
			  type="TestAppServer">
	  </server>
	</servers>
	