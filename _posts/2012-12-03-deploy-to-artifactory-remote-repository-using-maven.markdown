---
author: chintohere
comments: true
date: 2012-12-03 06:11:50+00:00
layout: post
slug: deploy-to-artifactory-remote-repository-using-maven
title: Deploy to Artifactory (remote repository) using Maven
wordpress_id: 231
categories:
- java
- maven
tags:
- artifactory
- java
- maven
---

# Overview


Deploy to artifactory using maven.


# Configuration




## Add your repository server configuration to maven settings.xml


This needs to be done only once. If the repository is already configured in your user settings.xml, skip this step.

Add below configuration to your settings.xml

Below configuration can be obtained from your artifactory








`<``server``>`




`  <``id``>{repo-id}</``id``>`




`  <``username``>{repo-username}</``username``>`




`  <``password``>{password/encrypted password}</``password``>`




`</``server``>`








More info here



	
  * Artifactory - [http://wiki.jfrog.org/confluence/display/RTF20/Using+Secured+Passwords+in+Settings.xml](http://wiki.jfrog.org/confluence/display/RTF20/Using+Secured+Passwords+in+Settings.xml)

	
  * Maven - [http://maven.apache.org/settings.html](http://maven.apache.org/settings.html)




## Add maven-deploy-plugin to your pom










`<``plugin``>`




`  <``groupId``>org.apache.maven.plugins</``groupId``>`




`  <``artifactId``>maven-deploy-plugin</``artifactId``>`




`  <``version``>2.7</``version``>`




`</``plugin``>`








More info [http://maven.apache.org/plugins/maven-deploy-plugin/plugin-info.html](http://maven.apache.org/plugins/maven-deploy-plugin/plugin-info.html)


## Add remote (artifactory) repository to your POM










`<``distributionManagement``>`




`  <``repository``>`




`    <``id``>{repo-id}</``id``>`




`    <``name``>{repo-id}</``name``>`




`    <``url``>[http://](http://integ/){repo-host-name}/artifactory/{repo-url}</``url``>`




`  </``repository``>`




`</``distributionManagement``>`








More info at



	
  * Artifactory - [http://wiki.jfrog.org/confluence/display/RTF/Configuring+Deployment](http://wiki.jfrog.org/confluence/display/RTF/Configuring+Deployment)

	
  * Maven - [http://maven.apache.org/pom.html#Distribution_Management](http://maven.apache.org/pom.html#Distribution_Management)




# Deploy Using Maven


Running below command would deploy it to the default repository








`1.``mvn deploy`








In case of multiple repositories in pom, specify repository id.








`1.``mvn deploy -DrepositoryId`








More info at [http://maven.apache.org/plugins/maven-deploy-plugin/usage.html](http://maven.apache.org/plugins/maven-deploy-plugin/usage.html)
