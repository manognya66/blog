---
title: My First Intercepted Request in Burp Suite (OWASP Juice Shop)
layout: page
nav_order: 1
parent: Web Fundamentals
---

## What is Burp Suite?

**Burp Suite** is a web application security testing tool that acts as an intercepting proxy between a browser and a web server. It allows security testers to capture, inspect, and modify HTTP/HTTPS requests and responses in real time.

By observing this raw traffic, we can understand how browsers communicate with servers, identify hidden data like cookies and headers, and analyze how web applications handle user input.

This ability to intercept and analyze requests makes Burp Suite a fundamental tool for learning and performing web application security testing.

---

# My First Intercepted Request in Burp Suite (OWASP Juice Shop)

One of the most important moments in learning web security is seeing how a browser actually talks to a web server.

In this lab, I used **Burp Suite** to intercept the very first HTTP request sent from my browser to the OWASP Juice Shop application running on `localhost`.

This helped me understand:

- How HTTP requests look in real life
- What headers are sent by the browser
- How tools like Burp act as a man-in-the-middle proxy

---

## Lab Setup

- OWASP Juice Shop running on: `http://localhost:3000`
- Firefox configured with **FoxyProxy**
- Burp Suite running as an intercepting proxy on `127.0.0.1:8080`

Browser → Burp → Juice Shop

---

## What is Burp Suite Doing Here?

Burp Suite sits between the browser and the server.

Instead of the request going directly like this:
-> Browser → Juice Shop
