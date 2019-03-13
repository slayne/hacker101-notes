---
title: Hacker101
tags: [Notebooks/HackerOne]
created: '2019-02-02T14:14:34.000Z'
modified: '2019-02-06T08:47:55.015Z'
---

# Hacker101

## Cookies
Cookies added for a subdomain can be accessed by this subdomain and all its children

Two flags for cookies :
* Secure : only https page
* HTTPOnly : js cant read cookie

This info is found in the `Set-Cookie` header.

Cookie domain scoping is often a source of trouble 

## Encoding / mime sniffing 

You can try using different encoding for xss ex : UTF-7 .

Or inject code into fake images for instance
works if the mimetype is incorrectly checked

## Cross-Site Request Forgery (CSRF)

CSRF is when an attacker tricks a victim into going to a page they controll which then submits some data to the target site as the victim.

One of the most common vuln > enables a lot of other vulns (rXSS)

To mitigate this use CSRF tokens

## XSS

### Recognition

1. Figure out where it goes : tag attribute ? String into a script tag ?
2. Figure out any special handling : Url turned into links ?
3. How are special chars handled ? try `<>:;"'` 

Try to break out of attributes to inject dom .

### Cheat Sheet

* `"><h1>test</h1>`
* `'alert(1)+'`
* `"onmouseover="alert(1)`
* `http://"onmouseover="alert(1)`

## Auth-z bugs

Acess pages that you're not supposed to see 

example : change page id nb `url.com/page?id=3` 

Test all entry points you can use as a privileged user with a non privileged user.


# Directory traversal

By controlling path construction you're able to to walk the filesystem. For instance use of  `.`and `..` in stuff we can inject. Often leads to arbitrary file reads/writes.

# Command injection

When a page let you use a system command such as ping you can try to inject more commands by using `'echo test;'`or even `| echo test`

# SQL Injection

Easy to mitigate but webapps perform a lot of queries we just have to find one bug

## Identification
* `'Or 1='1 --` > This returns all rows (constant true)
* `'AND 0='1 --`   > This returns no rows (constant false)  
* `'"><h1>test` 

Usage of these simple payloads can help identify sqli

## Exfiltration

Usage of `UNION` is generally one of the simplest way to get data out of the system.

EX:
``` sql
select foo,bar,baz from some_table where foo='1' union select 1?3?4; --';
```

## Blind SQLi

When you can't direclty see the result of the query
good tutorial : [link](https://zestedesavoir.com/tutoriels/945/les-injections-sql-le-tutoriel/les-injections-sql-en-aveugle/blind-sql-injection/)

## Detecting database

It is important to detect which db engine you're facing google for more details
