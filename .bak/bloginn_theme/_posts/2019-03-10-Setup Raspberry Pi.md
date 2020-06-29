---
layout: post
title: "Setup Raspberry Pi"
date: 2019-03-10
banner_image: Raspberry Pi.jpg
tags: [Raspberry Pi, Development]
---

* [Official site](https://www.raspberrypi.org/)  
* [Download Raspbian(OS for Raspberry Pi based on Debian)](https://www.raspberrypi.org/downloads/raspbian/)  
* [Flash Raspbian to micro SD card](https://www.balena.io/etcher/)  

<!--more-->

* Default login/password
```bash
login:pi
password:raspberry
```
* Configuration  
```bash
$ sudo raspi-config
```
* Copy host's SSH public key to Raspberry Pi  
```bash
$ cat ~/.ssh/id_rsa.pub | ssh <username>@<ip-address> 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys'
```
