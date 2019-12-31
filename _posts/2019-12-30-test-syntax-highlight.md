---
layout: post
title: "Connect to Office 365 Function"
date: 2019-12-30 12:00:00
categories: Test
featured_image: /images/bride.jpg
---

## Testing Syntac Highlighting

Markdown

''' powershell
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
'''

## Liquid 

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