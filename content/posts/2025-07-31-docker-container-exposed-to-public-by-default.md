---
title: Docker container exposed to public by default
date: 2025-07-31T17:15:01.883Z
---
Recently i found security issue in my server which causes sine apps in docker can be accessed bypassing the firewall *ufw*. This made me panic shock for a bit, which later lead me to new knowledge and luckily it is not a production server.

This happened because, by default, Docker binds the port directly using iptables, which bypasses UFW. If we expose it like 3000:3000, it's open to the outside. To fix that, we just need to bind it to localhost instead using 127.0.0.1:3000:3000. That way, it's only accessible locally.