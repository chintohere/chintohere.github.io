---
author: chintohere
comments: false
date: 2008-06-13 02:36:00+00:00
layout: post
slug: recursively-delete-files-within-all-sub-directories-in-dos
title: Recursively Delete files within all sub directories in DOS
wordpress_id: 17
categories:
- dos
- tech
tags:
- dos
- quickfix
- tech
- windows
---

Ever wondered how to delete files matching a certain patten from within all sub-directories in DOS (aka Windows).

Simple

At your command prompt type simply DEL /S  *.ext
eg:
To delete all .bak files within D:Workspace

`D:/workspace>del/s *.bak
`

But be careful.. there is no confirmation dialog.
