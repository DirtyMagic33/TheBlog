---
layout: post
title: "Connect to Office 365 Function"
date: 2014-07-21 12:00:00
categories: Office 365
featured_image: /images/391660.jpg
---

Using PowerShell to manage Office 365 is very um, for lack of a better word, powerful. And although more functionality has been to the UI there are tasks that still need be done using PowerShell. Also if you need to do any sort of bulk administration tasks PowerShell is where it’s at.

I’m going to assume you have already downloaded and installed the software required to manage Office 365 and that you have an account with the appropriate permissions. To connect PowerShell to Office 365 there are a few commands required, which by the way I can never remember so I’m always cutting and pasting. If you manage many different tenants, as do I, you’ll find that you are constantly connecting and disconnecting from each environment. Sometimes the connection process takes more time and more commands than what you’re trying to do – like resetting a password or granting permission to a mailbox. I wanted a way to quickly and easily connect and disconnect my session.

I’ve created functions to ease other PowerShell related tasks, I should be able to do the same is this case. This could then be added to a module so that the commands are available when I start PowerShell.

I will be creating two functions, one used to create and connect a session (Connect-Office365), and the other to close the session (Disconnect-Office365). These will be simple functions with no parameters or anything. Bear in mind that these functions are only designed to connect to Exchange Online and Office 365. If you would like to connect to SharePoint Online and Lync Online you’ll have to add those commands to the script or create separate functions for those services.

## The Connection Function

The connect script starts out by setting PowerShell’s execution policy to RemoteSigned. If it is set to anything other than RemoteSigned or Unrestricted you will encounter errors.

```powershell
Set-ExecutionPolicy RemoteSigned
```

The next step in the script is to create a variable to store your Office 365 credentials. When the function is run a dialog box will appear and you will need to enter your Office 365 username and password.

Code goes here.

This creates a remote PowerShell session to Exchange Online. Note the use of the credential object we created in the first step.

Code goes here.

This next line imports the newly created session. Here is where it got a little tricky for me. Normally when connecting to Office 365 not using a script you would just use Import-PSSession $Session. But when doing that inside of a script, you still get connected, but when you try to run an Exchange command like Get-Mailbox you will get an error stating that this is not recognized as a cmdlet. Looking back at the output of the script I noticed this bit of info.

WARNING: Proxy creation has been skipped for the following command: ‘TabExpansion’, because it would shadow an existing local command. Use the AllowClobber parameter if you want to shadow existing local commands.

The AllowClobber parameter imports the specified commands even if they have the same name as existing commands. I’m always reminded of The Thing when I see that parameter.

code goes here.

This last command loads the Office 365 cmdlets such as Get-MsolDomain and New-MsolUser.

Code goes here.

You can view the cmdlets in this module using the following command.

Code goes here.

The entire function looks like this.

Code goes here.

## Closing Your PowerShell Session

You may be wondering why I even bothered to create this function. You could just close the PowerShell window and be on your way, right? Yes, but that wouldn’t be the proper way. You’re session would remain open for the next fifteen minutes or so. Office 365 has a maximum of three connections per administrator account. You could possibly run into a situation where you’d get an error when trying to connect if stale sessions were left open; it’s best practice and dead simple to do so.

Closing the session is just one line. We pipe the Get-PSSession cmdlets to Where-Object looking for sessions that contain “outlook.com”. The results are then piped to the Remove-Session cmdlet.

Code goes here.

The entire disconnect function looks like this.

Code goes here.

## Using the Functions

In order to have these functions available in you PowerShell you need to add them to a module. If you don’t have an existing one here’s how to create one.

Open Notepad and paste the two functions. Save the file as something like MyTools.psm1 in the following directory “C:\Users\username\WindowsPowerShell\Modules\MyTools”
You can call the file whatever you like, just remember that the file and the folder that it goes into must have the same name. Now use tab complete to quickly and easily connect to Office 365 in PowerShell.
