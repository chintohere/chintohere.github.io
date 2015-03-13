---
author: chintohere
comments: true
date: 2013-12-19 04:24:26+00:00
layout: post
slug: java-lang-illegalstateexception-no-active-session-context-when-using-seam-components-from-within-an-mdb
title: 'java.lang.IllegalStateException: No active session context when using Seam
  components from within an MDB'
wordpress_id: 252
---

[java]
java.lang.IllegalStateException: No active session context
at org.jboss.seam.security.Identity.instance(Identity.java:157)
[/java]

Have you ever seen this error while trying to use seam services from within an MDB. This is because MDB invocations do not have any seam contexts or session initialised as these requests are initiated by the server and are not coming through Seam/Identity filters.

A quick solution for this would be have an EJB interceptor which would take care setting up Seam for you. This would intialize seam context before your **onMessage** call and end it after it.

[java]
package com.example.security.mdb;

import java.util.HashMap;
import java.util.Map;

import javax.interceptor.AroundInvoke;
import javax.interceptor.InvocationContext;
import javax.jms.Message;
import javax.jms.ObjectMessage;
import javax.security.auth.login.LoginException;

import org.jboss.seam.Component;
import org.jboss.seam.contexts.Lifecycle;
import org.jboss.seam.log.Log;
import org.jboss.seam.log.Logging;

import com.hrx.rasp.ejb.signon.RaspIdentity;
import com.hrx.rasp.security.RaspSessionServiceLocal;

public class MDBSeamSecurityInterceptor
{
	private Log logger = Logging.getLog(MDBSeamSecurityInterceptor.class);

	@AroundInvoke
	public Object onMessageInterceptor(InvocationContext ctx) throws Exception
	{
		Map<String, Object> session = new HashMap<String, Object>();
		Map<String, Object> appCtx = new HashMap<String, Object>();
		try
		{
			Lifecycle.beginSession(session, appCtx);
			Lifecycle.beginCall();

			if (ctx.getMethod().getName().equals("onMessage"))
			{
				logger.debug("onMessage method intercepted");

                                //e.g. optional seam identiy initialisation
                                RaspIdentity identity = RaspIdentity.getInstance();
               			identity.setSessionId(sessionId);
		        	identity.getCredentials().setUsername("dummy");
			        identity.getCredentials().setPassword("dummy");
	        		identity.authenticate();

			}

			return ctx.proceed();
		}
		catch (Exception e)
		{
			logger.fatal("failing to authenticate MDB with seam identity", e);
			throw new RuntimeException(e);
		}
		finally
		{
			Lifecycle.endCall();
		}

	}

}

[/java]
