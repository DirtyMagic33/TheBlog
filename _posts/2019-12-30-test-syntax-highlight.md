---
layout: post
title: "Testing Syntax Highlights"
date: 2019-12-30 12:00:00
categories: Test
featured_image: /images/bride.jpg
---

Sample PowerShell code to see how it is being displayed.

{% highlight powershell %}
[System.Collections.ArrayList]$ArrayList = @()

Foreach ($item in $collection)
{
	$obj = "" | select 'Property1','Property2','Property3'
	
	$obj.Property1 = $value1
	$obj.Property2 = $value2
	$obj.Property3 = $value3
	
	$ArrayList += $obj 
	$obj = $null
}

$ArrayList
{% endhighlight %}


{% highlight powershell %}
configuration WebServerBaseline
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Import-DscResource -ModuleName xWebAdministration

    node localhost
    {
        WindowsFeature WebServer
        {
           Ensure = "Present"
           Name   = "web-server"
        }

        WindowsFeature WebMgmtTools
        {
           Ensure = "Present"
           Name   = "Web-Mgmt-Tools"
        }

        WindowsFeature NETNonHTTPActiv
        {
           Ensure = "Present"
           Name   = "NET-Non-HTTP-Activ"
        }

        File Globomantics
        {
            Ensure          = "Present"
            DestinationPath = "$env:systemdrive"+"\Globomantics"
            Type            = "Directory"
        }

        xWebAppPool GlobomanticsAppPool
        {
            Name = 'Globomantics'
            Ensure = 'Present'
            ManagedRuntimeVersion = 'v4.0'
            IdleTimeoutAction = 'Terminate'
            cpuAction = 'ThrottleUnderLoad'
            autoStart = $true
            restartRequestsLimit = 0
            enable32bitApponWin64 = $false
        }
    }
}
{% endhighlight %}