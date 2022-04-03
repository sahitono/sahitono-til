---
title: Check who use port
date: 2021-11-11T08:59:21.765Z
tags:
  - powershell
  - network
cover:
  image: ""
  caption: ""
---
This is a powershell command to check who use selected port
```powershell
Get-Process -Id (Get-NetTCPConnection -LocalPort YourPortNumberHere).OwningProcess
```