---
layout: post
title:  "L4 vs L7 Load Balancers"
date:   2020-05-05 20:05:00 -0700
categories: web load-balancing
---

Just heard a great talk today about cloud load balancing. Load balancer has two main categories,
hardware load balancer (Layer-4) and software load balancer (Layer-7)

### Layer-4 Hardware Load Balancer

These balancer are capable of balancing the request load on a TCP/IP layer.
Accepting requests from a single public IP address and distribute loads/proxy requests
into multiple VMs using the Network Address Translation (NAT). Layer-4 load balancers are super
performant, but on the other hand, they have very limited computational power, and thus, are
not capable of inspecting HTTP context. Distributing loads based on HTTP content (e.g. "Host: "
HTTP header, "Affinity" Cookies) is impossible.

### Layer-7 Software Load Balancer

Unlike L4, L7 are very expensive since they are running on a computational unit, a virtual
mahcine. There are some popular L7 load balancers, such as Nginx, Apache. Using Layer-7 is reverse
proxying requests into different processes in the same VM, or into different VM instances. They are
super powerful, can process requests based on its HTTP context. However, as you can image, these
load balancers are expensive and requires a comparably high maintanance cost (as VMs are
sophisticated and you may need to constantly upgrade the distro and software).

### Why Not Domain Name Server (DNS)

Well, DNS is slow and between each of them, there's a Time To Live (TTL) config. This config will
makes a Domain->IP entry in a DNS cached for a while. The IP address needs to be relatively stable
if it is a destination in a DNS entry. Constantly updating the DNS to achieve the load balancing
purpose, it is just not realistic.
