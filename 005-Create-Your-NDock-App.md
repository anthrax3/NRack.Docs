# Create Your NDock App

> __Keywords__: NDock, NDock App, AppServer


## Get NDock

The latest version of NDock is available as the [NDock NuGet package](https://www.nuget.org/packages/NDock/). If you are not familiar with the NuGet Package Manager, we encourage you to read the [NuGet Overview](http://docs.nuget.org/consume/overview).

### Installing the NDock NuGet Package

You can install the NDock package by right-clicking on the References folder of your project and selecting Manage NuGet Package...

![nuget reference](images/nuget.png)

### Installing from Package Manager Console

Alternatively, you can install NDock by running the following command in the [Package Manager Console](https://www.nuget.org/packages/NDock/).

	PM> Install-Package NDock


## Create Your NDock AppServer

Define a class base on the NDock AppServer base class, and implement some required methods.
And add an attribute AppServerMetadata with its identiry name. The identity name will be used in NDock configuration.


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
	
	
	
## More Methods can be Overrided of NDock AppServer

### Setup method for initializing code

		protected override bool Setup(IServerConfig config, ExportProvider exportProvider)
        {
            return true;
        }

### OnPreStart method for the code to be executed before start

		protected override bool OnPreStart()
		{
			return true;
		}
		
### OnStarted method for the code to be executed after start

		protected override bool OnStarted()
		{
			return true;
		}
		
### OnPreStop method for the code to be executed before stop

		protected override bool OnPreStop()
		{
			return true;
		}
		
### OnStopped method for the code to be executed after stop

		protected override bool OnStopped()
		{
			return true;
		}
		
### CanBeRecycled method to return whether the app can be recycled now

		public override bool CanBeRecycled()
        {
            return true;
        }


## Enable Logging in NDock


## Deployment and Configuration


