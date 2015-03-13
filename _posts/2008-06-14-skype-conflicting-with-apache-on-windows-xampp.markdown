---
author: chintohere
comments: false
date: 2008-06-14 18:36:00+00:00
layout: post
slug: skype-conflicting-with-apache-on-windows-xampp
title: Skype conflicting with Apache on Windows (XAMPP)
wordpress_id: 18
categories:
- tech
---

If you use XAMPP for web development and have skype running at the same time. Specifically if you start Skype before you start apache, you will realize that you are getting blank page's on your webserver. If you notice the apache console, There should be an error on the lines.  
  
`  
(OS 10048)Only one usage of each socket address (protocol/network address/port)  
is normally permitted. : make_sock: could not bind to address 0.0.0.0:80  
no listening sockets available, shutting down  
Unable to open logs  
`  
  
Quick fix: Start apache before Skype(i.e. take out skype out of startup)  
  
Better Fix: Go into Skype>Tools>Options>Advanced>Connection and Uncheck 'Use port 80 and 443 as alternatives for incoming connection'  
  
If you have 'Firewall' like I do. Open the port specified by Skype on the same options page for TCP/UDP for the best performance,.  
  
If you have a router based NAT firewall .. then do it through the web console, or if it's Zone Alarm or any other windows based firewall.. add the port number to exceptions.  
  
Some usefull links  
  
[http://www.skype.com/help/guides/firewall.html](http://www.skype.com/help/guides/firewall.html)  
[http://support.skype.com/index.php?_a=knowledgebase&_j=questiondetails&_i=148](http://support.skype.com/index.php?_a=knowledgebase&_j=questiondetails&_i=148)  
[http://forum.skype.com/lofiversion/index.php/t16779.html](http://forum.skype.com/lofiversion/index.php/t16779.html)
