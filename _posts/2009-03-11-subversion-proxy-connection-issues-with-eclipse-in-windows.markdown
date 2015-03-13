---
author: chintohere
comments: true
date: 2009-03-11 06:56:33+00:00
layout: post
slug: subversion-proxy-connection-issues-with-eclipse-in-windows
title: Subversion proxy connection issues with Eclipse (In windows)
wordpress_id: 65
categories:
- eclipse
- java
tags:
- eclipse
- java
- subclipse
- subversion
- subversive
---

If you are having issues connecting to your subversion repositories from Eclipse (May be with Subversive/Subclipse). Try the following.


## Enter proxy details into Subversion configuration:




### Open **servers** file in the following location






Window XP

    C:\Documents and Settings\MyUserId\Application Data\Subversion\**servers**

Windows Vista

    C:\Users\Clientside\AppData\Roaming\Subversion\**servers**





### Update following lines at the end of file



    
    [global]
    http-proxy-exceptions = yourproxy exceptions (e.g. dev.company.com.au)
    http-proxy-host = yourproxyhost (e.g. proxy.company.com.au)
    http-proxy-port = your proxy port (e.g. 8080)
    http-proxy-username = proxyusername
    http-proxy-password = proxypassword



_This step might not be needed all the time _


## Update Eclipse Proxy settings





**Windows > Preferences**




Type '**proxy**' in the filter text box. Go to 'Network Connections' config page. Choose manual proxy configuration and Update the proxy details.



