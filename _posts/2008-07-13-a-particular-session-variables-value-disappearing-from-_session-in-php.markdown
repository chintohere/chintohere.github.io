---
author: chintohere
comments: true
date: 2008-07-13 14:03:00+00:00
layout: post
slug: a-particular-session-variables-value-disappearing-from-_session-in-php
title: A particular session variable's value disappearing from $_SESSION in PHP
wordpress_id: 23
categories:
- php
- web development
tags:
- php
- tech
- web development
---

A particular session variable's value disappearing from $_SESSION in PHP... ??

Just check to make sure you DON'T have register_globals turned On. This took me a few hour's to figure out..

Example scenario..
Form Bean class
`
class FormBean
{
public $email;
public $name;
}
`

page1.php
`
$form = new FormBean();
$form->email = "someone@something.com.au";
$_SESSION['form'] = serialize($form);
header("location:page2.php");
`

page2.php
`
$form =NULL;
if(isset($_SESSION['form']))
{
$form = unserialize($_SESSION['form']);
}
echo $form->email;
`

Expected to print "someone@something.com.au" right. Usually it does. If it doesn't and you see that all other session variables are intact except 'form', then it's time to look at your 'register_globals' setting. One of my client uses this pretty lax hosting which had this on what it has done is ....

page2.php
`
**$form =NULL;** //This sets the form bean to NULL.. wherever it is stored. Throughout the entire website. (Even IN $_SESSION)`

` `

`if(isset($_SESSION['form']))
{
$form = unserialize($_SESSION['form']);
}
echo $form->email;
`

So the lesson learnt for me was... Just check to make sure register_globals is Off whenever you switch to new hosting.. coz that is pure EVIL.

How you can turn it off.. There are two different ways.



	
  1. [ini_set](http://www.php.net/ini_set)


	
  2. .[htaccess](http://www.askapache.com/php/custom-phpini-tips-and-tricks.html)


This also makes me feel that PHP's OOP implementation is either misleading , buggy or at least fundamentally different to other OOP languages like Java or C#.

Consider this in Java:
FormBean.java
`
class FormBean
{
public String email;
}
`

TestFormBean.java
`
class TestFormBean
{
public static void main(String[] args)
{
FormBean form1 = new FormBean(); //Create new form bean
form1.email = "someone@something.com.au"; //populate form bean`

`FormBean form2 = form1; //Assign created form bean object to another reference variable
form1 = null;

`

` System.out.println(form2.email);

//would still print "someone@something.com.au"
//i.e. Just setting one reference to NULL won't kill its object instance.
}
}`
I have tested similar code with PHP though... I have only realised **register_globals** seems to affect the ways objects and their references are handled. Like setting one reference of an object to NULL killing the object instance, which essentially renders all my other references useless.
