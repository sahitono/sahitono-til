---
title: SuperMap iServer Reverse Proxy
date: 2022-09-07T02:54:20.688Z
tags:
  - supermap
  - work
  - gis
---
Recently, i've been struggling to deploy SuperMap iServer live behind reverse proxy. The problem was caused by host received by tomcat is not the original host and iServer generate its html resources respective to the hostname.

So, we need to use RemoteIpValve like below to tell the tomcat to use the hostname from `x-forwarded-proto` as the hostname.

```xml
<Valve className="org.apache.catalina.valves.RemoteIpValve" protocolHeader="x-forwarded-proto" />
```

This configuration can be placed under Host tag in server.xml file.