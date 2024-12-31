+++
title = "A Minimal Guide For Nmap"
description = "There are five main phases of hacking, and among them, the most essential one is gathering information. First you need to find a weakness, without it you’re aimless."
date = 2023-01-08
authors = ["Mazdak Pakaghideh"]
[taxonomies]
tags = ["security", "nmap"]

[extra.comments]
id = 113747380646578451
+++

![Nmap](https://mazdak.dev/wp-content/uploads/2023/01/nmap-1.png)
_www.abrictosecurity.com_

There are five main phases of hacking, and among them, the most essential one is gathering information.

> _First you need to find a weakness, without it you’re aimless._

or in a more technical way Reconnaissance & Scanning. Nmap is a popular open-source software used for both active reconnaissance and scanning. It can scan through different ports of a particular server and by that it gives us a lot of information.

{% alert(caution=true) %}
Note: This utility should not be used in illegal activities. Instead, you can use it by participating in CTF platforms such as **[Hack The Box](https://www.hackthebox.com/)**.
{% end %}

## So basically how?

Each port number is dedicated to a particular service running in the background of a system. These services can be accessed by their unique port numbers, and from them, a lot of information such as service name, version, and vulnerabilities can be gained. Knowing this information is essential for identifying potential weaknesses and determining if they are exploitable.

## Nmap Features

Gaining information about services is just one of the many abilities of Nmap. In addition to these features, It offers a variety of different features.

Which includes:

- Scan for vulnerabilities
- Host discovery
- OS detection
- Firewall detection
- Identify open ports
- NSE Scripts

## Installation

Nmap could be easily installed in Unix/Linux-based Operating Systems by using the commands below. Or by visiting **[Nmap’s official download page](https://nmap.org/download.html)**.


```sh
$ sudo apt install namp # Debian, Ubuntu
$ sudo pacman -S nmap # Arch Linux
$ sudo snap install nmap # Fedora
$ sudo brew install nmap # MacOS
```

## Nmap Commands

Before proceeding, here is Nmap’s general commands structure:

```
$ nmap [Scan-type] [Options] [Target]
```

### Scanning Specific Systems

This command scans 1000 usual ports by default.


```sh
$ nmap [IP] or [Hostname]
$ nmap [IP 1] [IP 2] [IP n]

$ nmap 192.168.1.104 #Example
```

An Asterisk (\*) could be used to scan all of the subnets.

```
$ nmap 192.168.1.*
```

A hyphen (-) could be used to specify a range of IP address.

```
$ nmap 192.168.0.0–255
```

### Stealth Scan

![](https://img.wonderhowto.com/img/36/13/63578617777373/0/build-stealth-port-scanner-with-scapy-and-python.w1456.jpg)
_By null-byte.wonderhowto.com_

Although just like any other TCP 3-Way-Handshake a stealth scan is started by sending an SYN packet to the server, It has one huge difference. a stealth scan never completes as like the normal 3-Way-Handshake. Accordingly, it’s hard for the target to determine the scanning system.


```sh
$ nmap -sS [Target]
$ nmap -sS 192.168.1.5
```

### Retrieving All IP Addresses In a Network

The commands below scan for all connected devices in a particular network using the TCP SYN scan method by providing a subnet range.


```sh
$ nmap -sS [The_Subnet]
$ nmap -sS 192.168.1.0/24 #Example
```

### Service Version Scanning


```sh
$ nmap -sV [Target]
$ nmap -sV scanme.nmap.org #Example 
```

### OS Scanning

> One of Nmap’s best-known features is remote OS detection using TCP/IP stack fingerprinting. Nmap sends a series of TCP and UDP packets to the remote host and examines practically every bit in the responses. After performing dozens of tests such as TCP ISN sampling, TCP options support and ordering, IP ID sampling, and the initial window size check, Nmap compares the results to its `nmap-os-db` database of more than 2,600 known OS fingerprints and prints out the OS details if there is a match.nmap.org
> 
> <cite>nmap.org</cite>

```sh
$ nmap -O [Target]
$ nmap -O scanme.nmap.org #Example
```

### Aggressive Scanning

This mode will enable OS detection (-O), Version Detection (-sV), Script scanning (-sC) and traceroute (–traceroute) altogether.


```sh
$ nmap -A [Target]
$ nmap -A scanme.nmap.org #Example
```

### Port Scanning

By using the -p parameter, the port scan could be easily performed.


```sh
$ nmap -p [Port] [Target]
$ nmap -p 22 192.168.1.5 #Example
```

You can even specify the type of your desired port.

```sh
$ nmap -p T:80
```

A range of ports could be also scanned by Nmap.

```sh
$ nmap -p 80-443 192.168.1.5
```

### Scanning From a File

This type of scan is very useful when automating. For instance, a script can crawl over a website and save all the servers in a particular file. So that Nmap could use this file to scan all the crawled servers and even more it could be used to save the results in a specific file.


```sh
 $ nmap -iL [Path_To_File]
 $ nmap -iL ./servers.txt > result.txt #Example
```

### Vulnerability Scanning

There are third-party scripts used for scanning vulnerabilities in Nmap. Among them the most well-known one is[Nmap-Vulners](https://github.com/vulnersCom/nmap-vulners). You can use the commands below for installing and using this script.


```sh
# Navigating to the Nmap scripts directory

$ cd /usr/share/nmap/scripts/

# Cloning the git repository

$ git clone https://github.com/vulnersCom/nmap-vulners.git

# NSE scripts usage

$ nmap -sV --script vulners [--script-args mincvss=<arg_val>] <target>

# Example

$ nmap -sV --script nmap-vulners/ 192.168.1.5
```

The post [A Minimal Guide For Nmap](https://mazdak.dev/a-minimal-guide-for-nmap/) appeared first on [mazdak.dev](https://mazdak.dev).