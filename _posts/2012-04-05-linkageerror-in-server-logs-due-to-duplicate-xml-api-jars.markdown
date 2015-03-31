---
author: chintohere
comments: true
date: 2012-04-05 00:06:57+00:00
layout: post
slug: linkageerror-in-server-logs-due-to-duplicate-xml-api-jars
title: LinkageError  in server logs due to duplicate xml api jars
wordpress_id: 170
categories:
- java
- jboss
- maven
tags:
- java
- jboss
- maven
---

Ever seen this  linkage error. This is caused by various reasons of duplicate jars containing xml-apis.

I had this issue when I included Apache POI jars (poi-ooxml-schemas) which in turn included stax-api jars **(geronimo-stax-api_1.0_spec.jar, stax-api.jar)** and xml-api's **(xml-api.jar, xmlbeans.jar)**.

Excluding them from your dependency would solve the issue.


## Exclude Example


        <exclusions>
                <exclusion>
                        <artifactId>stax-api</artifactId>
                        <groupId>stax</groupId>
                </exclusion>
                <exclusion>
                        <artifactId>geronimo-stax-api_1.0_spec</artifactId>
                        <groupId>org.apache.geronimo.specs</groupId>
                </exclusion>
                <exclusion>
                        <artifactId>xml-apis</artifactId>
                        <groupId>xml-apis</groupId>
                </exclusion>
                <exclusion>
                        <artifactId>dom4j</artifactId>
                        <groupId>dom4j</groupId>
                </exclusion>
        </exclusions>


## LinkageError Stack Trace


        java.lang.LinkageError: loader constraint violation in interface itable initialization: when resolving method "com.sun.xml.bind.DatatypeConverterImpl.parseQName(Ljava/lang/String;Ljavax/xml/namespace/NamespaceContext;)Ljavax/xml/namespace/QName;" the class loader (instance of org/jboss/classloader/spi/base/BaseClassLoader) of the current class, com/sun/xml/bind/DatatypeConverterImpl, and the class loader (instance of ) for interface javax/xml/bind/DatatypeConverterInterface have different Class objects for the type javax/xml/namespace/QName used in the signature
                at com.sun.xml.bind.v2.runtime.JAXBContextImpl.(JAXBContextImpl.java:227)
                at com.sun.xml.bind.v2.ContextFactory.createContext(ContextFactory.java:84)
                at com.sun.xml.bind.v2.ContextFactory.createContext(ContextFactory.java:66)
                at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
                at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:39)
                at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:25)
                at java.lang.reflect.Method.invoke(Method.java:597)
                at javax.xml.bind.ContextFinder.newInstance(ContextFinder.java:214)
                at javax.xml.bind.ContextFinder.find(ContextFinder.java:375)
                at javax.xml.bind.JAXBContext.newInstance(JAXBContext.java:574)
                at org.jboss.ws.core.jaxws.CustomizableJAXBContextFactory.createContext(CustomizableJAXBContextFactory.java:90)
                at org.jboss.ws.core.jaxws.JAXBDeserializer.getJAXBContext(JAXBDeserializer.java:96)
                at org.jboss.ws.core.jaxws.JAXBDeserializer.deserialize(JAXBDeserializer.java:66)
                at org.jboss.ws.core.binding.DeserializerSupport.deserialize(DeserializerSupport.java:61)
                at org.jboss.ws.core.soap.XMLContent.unmarshallObjectContents(XMLContent.java:179)
                at org.jboss.ws.core.soap.XMLContent.transitionTo(XMLContent.java:96)
                at org.jboss.ws.core.soap.SOAPContentElement.transitionTo(SOAPContentElement.java:140)
                at org.jboss.ws.core.soap.SOAPBodyElementDoc.transitionTo(SOAPBodyElementDoc.java:85)
                at org.jboss.ws.core.soap.SOAPContentElement.getObjectValue(SOAPContentElement.java:172)
                at org.jboss.ws.core.EndpointInvocation.transformPayloadValue(EndpointInvocation.java:273)
                at org.jboss.ws.core.EndpointInvocation.getRequestParamValue(EndpointInvocation.java:115)
                at org.jboss.ws.core.EndpointInvocation.getRequestPayload(EndpointInvocation.java:135)
                at org.jboss.ws.core.server.DelegatingInvocation.getArgs(DelegatingInvocation.java:80)
                at org.jboss.wsf.container.jboss50.invocation.InvocationHandlerEJB3.invoke(InvocationHandlerEJB3.java:93)
                at org.jboss.ws.core.server.ServiceEndpointInvoker.invoke(ServiceEndpointInvoker.java:221)
                at org.jboss.wsf.stack.jbws.RequestHandlerImpl.processRequest(RequestHandlerImpl.java:468)
                at org.jboss.wsf.stack.jbws.RequestHandlerImpl.handleRequest(RequestHandlerImpl.java:293)
                at org.jboss.wsf.stack.jbws.RequestHandlerImpl.doPost(RequestHandlerImpl.java:203)
                at org.jboss.wsf.stack.jbws.RequestHandlerImpl.handleHttpRequest(RequestHandlerImpl.java:129)
                at org.jboss.wsf.common.servlet.AbstractEndpointServlet.service(AbstractEndpointServlet.java:85)
                at javax.servlet.http.HttpServlet.service(HttpServlet.java:717)
                at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:290)
                at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:206)
                at org.jboss.web.tomcat.filters.ReplyHeaderFilter.doFilter(ReplyHeaderFilter.java:96)
                at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:235)
                at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:206)
                at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:235)
                at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:191)
                at org.jboss.web.tomcat.security.SecurityAssociationValve.invoke(SecurityAssociationValve.java:190)
                at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:525)
                at org.jboss.web.tomcat.security.JaccContextValve.invoke(JaccContextValve.java:92)
                at org.jboss.web.tomcat.security.SecurityContextEstablishmentValve.process(SecurityContextEstablishmentValve.java:126)
                at org.jboss.web.tomcat.security.SecurityContextEstablishmentValve.invoke(SecurityContextEstablishmentValve.java:70)
                at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:127)
                at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:102)
                at org.jboss.web.tomcat.service.jca.CachedConnectionValve.invoke(CachedConnectionValve.java:158)
                at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:109)
                at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:330)
                at org.apache.coyote.http11.Http11Processor.process(Http11Processor.java:829)
                at org.apache.coyote.http11.Http11Protocol$Http11ConnectionHandler.process(Http11Protocol.java:598)
                at org.apache.tomcat.util.net.JIoEndpoint$Worker.run(JIoEndpoint.java:447)
                at java.lang.Thread.run(Thread.java:662)
