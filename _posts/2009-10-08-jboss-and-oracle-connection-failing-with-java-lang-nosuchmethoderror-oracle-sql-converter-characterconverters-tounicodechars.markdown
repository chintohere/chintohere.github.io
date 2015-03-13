---
author: chintohere
comments: true
date: 2009-10-08 02:06:14+00:00
layout: post
slug: jboss-and-oracle-connection-failing-with-java-lang-nosuchmethoderror-oracle-sql-converter-characterconverters-tounicodechars
title: 'JBoss and Oracle connection failing with java.lang.NoSuchMethodError: oracle.sql.converter.CharacterConverters.toUnicodeChars'
wordpress_id: 80
categories:
- java
---

Ever saw some/none of the DB calls in jboss (4.2.3) and oracle (9i) failing with the following error. The exceptions can be all different types, but eventually caused by this following exception.

` .
.
Caused by: java.lang.NoSuchMethodError: oracle.sql.converter.CharacterConverters.toUnicodeChars([BI[CII)I
.
.`

This happened when I tried to switch databases this morning (both Oracle 9i) . Nothing fixed it till I replaced both the Driver jars(_nls_charset12-10.2.0.jar, ojdbc14-10.2.0.jar) _, preferrably from somwhere the connection is working, I took them from a colleague.  Or you can try and download the latest drivers as well. But make sure to delete your server **work** and **temp** directories.
