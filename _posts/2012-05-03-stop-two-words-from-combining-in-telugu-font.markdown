---
author: chintohere
comments: true
date: 2012-05-03 07:30:44+00:00
layout: post
slug: stop-two-words-from-combining-in-telugu-font
title: Stop two words from combining in telugu font
wordpress_id: 187
categories:
- fun
- web development
tags:
- telugu
---

Sometimes in Telugu font if you put two words next to each other without a space they combine.
e.g. మహేష్ + తొ = మహేష్తొ
But what we want is మహేష్​తొ

In such cases use a [zero width space](http://en.wikipedia.org/wiki/Zero-width_space) or invisible space in my words to stop them from combining.




	
  1. Type మహేష్

	
  2. Type zero width space using "Alt+8023" for MS word and unicode &#8023; for web 


	
  3. Then type తొ





This trick even works in word.



