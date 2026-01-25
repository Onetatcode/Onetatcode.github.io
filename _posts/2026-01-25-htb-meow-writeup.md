---
title: "Hack The Box: Solving 'Meow'"
date: 2026-01-25 11:00:00 +0500
categories: [CTF, HackTheBox]
tags: [htb, linux, easy, telnet]
---

## Introduction
Meow is a starting point for beginners on Hack The Box. It focuses on understanding basic service enumeration.

### Enumeration
I started with an Nmap scan:
```bash
nmap -sC -sV 10.10.10.x
