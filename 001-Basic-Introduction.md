# NRack Basic Introduction

> __Keywords__: NRack, Introduction

NRack is a server application container, which can be used for your back end services' hosting and management.


## Assemblies Introduction

* NRack.Base.dll： 		NRack basic common assembly, which is referenced by NRack container server and NRack application (NRack App);
* NRack.Server.exe: 	NRack container server. It can run as windows service or console application;
* NRack.Worker.exe:		NRack worker. If NRack's isolation mode is Process, NRack worker will work as carrier process for NRack App.


## Define Your NRack App

Define a class base on the NRack AppServer base class, and implement some required methods.
And add an attribute AppServerMetadata with its identiry name. The identity name will be used in NRack configuration.

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


## Basic Configuration

The xml file below is a full NRack configuration sample:

NRack.Server.exe.config	
	
	<?xml version="1.0" encoding="utf-8" ?>
	<configuration>
	  <configSections>
		<section name="nrack" type="NRack.Base.Configuration.NRackConfigSection, NRack.Base"/>
	  </configSections>
	  <appSettings>
		<add key="ServiceName" value="NRackService"/>
	  </appSettings>
	  <nrack>
		<servers>
		  <server name="TestApp"
				  type="TestAppServer">
		  </server>
		</servers>
	  </nrack>
	</configuration>
	

### The attribute value of "ServiceName" in the appSettings section defines the windows service name if the NRack server runs as Windows Service:

	<add key="ServiceName" value="NRackService"/>

	
### The configuration below means the NRack server has one NRack app defined whose name is "TestApp" and it's type name is "TestAppServer". The type name is defined in the NRack AppServer class's  attribute AppServerMetadata:

	<servers>
	  <server name="TestApp"
			  type="TestAppServer">
	  </server>
	</servers>
	
	
## Start NRack

The entry executable file is "NRack.Server.exe". You can double click it to run and then you will be asked for whether you want to run it directly or install it as Windows Service.

NRack.Server.exe also can accept additional parameter:


### Run it as console application directly:

	NRack.Server.exe -c


### Install it as Windows Service:

	NRack.Server.exe -i

	
### Uninstall the NRack Windows Service:

	NRack.Server.exe -u

	