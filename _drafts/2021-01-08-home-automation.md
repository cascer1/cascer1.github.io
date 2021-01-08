---
title: My home automation setup
tags: [homeassistant, truenas, freenas]
categories: [automation]
---

A few months ago I built a little home server running TrueNAS Core. Initially I got it to replace a server I was renting. The beginning setup was quite simple; some SMB shares so I could access files from my computer, a Plex mediaserver to stream my media locally, and NextCloud for accessing files remotely. Everything was topped off with an nginx proxy for dealing with SSL certificates from LE.

Then I happened across [Home Assistant](https://www.home-assistant.io)

Home Assistant is an open source tool that ties together [a whole bunch of connected devices](https://www.home-assistant.io/integrations). I found it when I was looking for a way to automatically read the energy meter from the utility company, which it turns out I can.


