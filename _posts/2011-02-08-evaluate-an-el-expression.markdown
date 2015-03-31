---
author: chintohere
comments: true
date: 2011-02-08 07:33:05+00:00
excerpt: Evaluate an EL expression (expression language) in java (i.e. not UI layer
  JSF/JSP)
layout: post
slug: evaluate-an-el-expression
title: 'Evaluate an EL expression '
wordpress_id: 109
categories:
- java
tags:
- EL
- java
- jsf
- seam
---

Once you start using EL heavily within your UI, eventually you will want to use it/evaluate it back in your EJB's and Seam/Spring components

There are three steps to evaluating an EL expression.

        //get current EL context
        javax.el.ELContext elContext = javax.faces.context.FacesContext.getCurrentInstance().getELContext();

        //get the expression factory (for seam). You can probably do ExpressionFactory.newInstance() if not using seam .
        javax.el.ExpressionFactory expressionFactory = org.jboss.seam.core.Expressions.instance().getExpressionFactory();

        //Create value expression as the EL I'm evaluating is a value e.g. #{bean.property} . Create MethodExpression if the EL is a method e.g. #{bean.method()}
        javax.el.ValueExpression valueExpression = expressionFactory.createValueExpression(elContext, elExpressionYouAreEvaluating, WhateverYouAreExpecting.class);

        // get value and dont' forget to cast.
        whateverYouAreExpecting = (WhateverYouAreExpecting) valueExpression.getValue(elContext);

Yup.. that's how convulted this is . It should more be like below

        //NOTE: imaginary code
        Object value = ExpressionFactory.getValue("#{bean.property}");

[That's what these guys are asking as well..](http://www.sfwk.org/Documentation/ELWishList)
