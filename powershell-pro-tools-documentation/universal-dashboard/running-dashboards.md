# Running Dashboards

## Command Line

Dashboards can be run from the command line by using the Start-UDDashboard cmdlet. This cmdlet accepts a port and dashboard to run. The port can be any valid port number not currently being used by the system. Multiple dashboards can be run in the same PowerShell session on different ports. Once a dashboard is started, you can get a list of running dashboards using the Get-UDDashboard cmdlet.

Running the following cmdlet would start a dashboard listening on port 1000.

`Start-UDDashboard -Port 1000 -Dashboard $MyDashboard`

You should be able to view your dashboard by visiting [http://localhost:1000](http://localhost:1000)

### Auto Reload

Auto-reloading a dashboard allows for faster dashboard development. When you have a script that contains Start-UDDashboard and specify the -AutoReload parameter, the dashboard will reload automatically when changes are made to the script. Simply save your script and the running dashboard will refresh. If you have a webpage open to your dashboard, it will reload automatically. It provides instant feedback with changes to your dashboard.

Currently, if there is an error within your script and the auto-reload fails, you will need to start the dashboard manually.

### Wait

The Wait parameter is specified if you would like the current PowerShell execution to block while the dashboard is running. This parameter is required for running in Azure and IIS.

## UniversalDashboard.exe

UniversalDashboard.exe is provided along with the UniversalDashboard PowerShell module. It can be found in the installation directory of both the net451 folder and netstandard2.0 folder. UniversalDashboard.exe can be used to start a dashboard by just running the executable. It requires that the dashboard PowerShell script be named dashboard.ps1 and found in the parent directory of the executable.

For example, if UniversalDashboard.exe is in net451, then dashboard.ps1 should be found in the parent folder of net451. 

![](/assets/wwwroot.png)

The license should be named license.lic and also placed in net451. 

![](/assets/iis-license)

## Hosting in Azure and IIS

To host a dashboard in Azure or IIS, you will need to deploy the entire module to your site or WebApp. In the root module directory, place your dashboard.ps1. You need to specify the -Wait parameter on Start-UDDashboard so that the script blocks and waits for requests in Azure or IIS. Specifying the port isn't necessary because Azure and IIS use dynamic port tunneling.

IIS requires that the [ASP.NET Core module](https://docs.microsoft.com/en-us/aspnet/core/hosting/aspnet-core-module) is installed.

When installing in Azure, you can place your license file, named license.lic, in the root directory and it will automatically be read by the module.

