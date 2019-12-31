---
layout: post
title: "Testomg Syntax Highlight"
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