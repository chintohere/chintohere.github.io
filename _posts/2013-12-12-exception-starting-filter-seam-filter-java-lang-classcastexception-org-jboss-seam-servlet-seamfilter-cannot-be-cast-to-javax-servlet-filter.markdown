---
author: chintohere
comments: true
date: 2013-12-12 00:43:03+00:00
layout: post
slug: exception-starting-filter-seam-filter-java-lang-classcastexception-org-jboss-seam-servlet-seamfilter-cannot-be-cast-to-javax-servlet-filter
title: 'Exception starting filter Seam Filter java.lang.ClassCastException: org.jboss.seam.servlet.SeamFilter
  cannot be cast to javax.servlet.Filter'
wordpress_id: 250
categories:
- java
- jboss
- maven
tags:
- java
- jboss
- seam
- servlet
- tomcat
---

`Exception starting filter Seam Filter java.lang.ClassCastException: org.jboss.seam.servlet.SeamFilter cannot be cast to javax.servlet.Filter`

Ever notice this error when deploying your application with Seam.

This usually happens due to two reasons.



	
  * You have duplicate seam jars in your application (e.g. EAR/lib and WAR/WEB-INF/classes/lib)

	
  * or

	
  * You have a servlet-api jar bundled as part of your app, which you never should as your web server has it (tomcat/jboss/geronimo etc)


Hope this helps someone.. coz I've stumbled into this and solved it couple of times.
