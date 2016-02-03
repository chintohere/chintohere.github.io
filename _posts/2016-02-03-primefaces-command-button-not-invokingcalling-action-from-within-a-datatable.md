---
layout: post
title: "Primefaces command button not invoking/calling action from within a datatable"
description: "Primefaces command button stops working inexplicabily within a datatable without any errors"
category: JSF
tags: [primefaces,jsf]
---
{% include JB/setup %}

There are multiple reasons an action button or link in primefaces stops working.

One of the best resources is this answer on (stackoverflow)[http://stackoverflow.com/questions/2118656/commandlink-commandbutton-ajax-backing-bean-action-listener-method-not-invoked].

If none of those apply to you start doing this.

    1. Put the command button outside of the data table with some dummy value. see if it works.
    
    2. If it works, you should start taking out all the attributes of the p:datatable till you get your command button/link working. For me it was **filteredValues**.


