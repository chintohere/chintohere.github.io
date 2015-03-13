---
author: chintohere
comments: true
date: 2013-03-11 07:13:29+00:00
layout: post
slug: jdk-jbosstomcat-ssl-issue-the-trusta
title: JDK (JBoss/Tomcat) SSL Issue - "the trustAnchors parameters must be non-empty"
wordpress_id: 235
categories:
- java
- jboss
tags:
- java
- jboss
- ssl
- tomcat
---

If you see this error in your logs, it just means that your JDK has not been able to locate the trustStore.


## Fix this in your user profile (JDK fix)


[java]
Caused by: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
	at java.security.cert.PKIXParameters.setTrustAnchors(PKIXParameters.java:183)
	at java.security.cert.PKIXParameters.(PKIXParameters.java:103)
	at java.security.cert.PKIXBuilderParameters.(PKIXBuilderParameters.java:87)
	at sun.security.validator.PKIXValidator.(PKIXValidator.java:55)
[/java]

You can verify this by typing this into console (command prompt in windows)

[shell]
C:\>keytool -list
keytool error: java.lang.Exception: Keystore file does not exist: C:\Users\John.Doe\.keystore
[/shell]

A simple fix for this can be to copy your default keystore supplied by java into your profile.

[shell]
C:\>copy %JAVA_HOME%\jre\lib\security\cacerts %USERPROFILE%\.keystore
1 file(s) copied.
[/shell]

This should put a default keystore into your profile, which you can play around with.

This by no means is the solution you should be using in server environments. There you are various ways to handle this at server level.

See below links for more info.

[http://docs.oracle.com/javase/6/docs/technotes/guides/security/jsse/JSSERefGuide.html#Features](http://docs.oracle.com/javase/6/docs/technotes/guides/security/jsse/JSSERefGuide.html#Features)

[http://www.herongyang.com/PKI/HTTPS-Java-Programs-Communicate-with-HTTPS-Server.html](http://www.herongyang.com/PKI/HTTPS-Java-Programs-Communicate-with-HTTPS-Server.html)

[http://www.oracle.com/technetwork/java/javase/tech/index-jsp-136007.html](http://www.oracle.com/technetwork/java/javase/tech/index-jsp-136007.html)


## Fix this for a java application (e.g. Application Server like JBoss)


Set the trust store location and password on the java executable using JVM arguments.

Arguments:
[shell]
-Djavax.net.ssl.trustStore=<TRUST_STORE_LOCATION>
-Djavax.net.ssl.trustStorePassword=<TRUST_STORE_PASSWORD> (default is 'changeit')
[/shell]

You can do this for Jboss by adding as similar instruction mentioned below to your /bin/run.bat

After placing my keystore in \server\\conf, I added this line to my run.bat.

[shell]
set "JAVA_OPTS=%JAVA_OPTS% -Djavax.net.ssl.trustStore=%JBOSS_HOME%\server\<JBOSS_PROFILE>\conf\.keystore -Djavax.net.ssl.trustStorePassword=changeit"
[/shell]
