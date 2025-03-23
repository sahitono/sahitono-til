---
title: Zen Browser Linux Geolocation Not Working
date: 2025-03-23T16:25:59.396Z
tags:
  - linux
---
This issue caused by missing geolocation api key for google and mozilla in the zen browser. The solution is to use beacondb api here 

1. open `about:config`
2. search geo.provider.network.url
3. change it to `https://api.beacondb.net/v1/geolocate`