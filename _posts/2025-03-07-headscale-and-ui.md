---
title: "Headscale and HeadscaleUI"
date: 2025-03-07 18:27:00 -0400
description: "Tailscale is fantastic, but self-hosting the Tailscale VPN controller is even more fantastic."
tags: [Computers, Technology, Headscale, HeadscaleUI, VPN, WireGuard, Homelab]
image: https://i.postimg.cc/3RRZ49zB/headscale3-header-stacked-left.png
---

Tailscale is a VPN that uses WireGuard, a VPN that uses newer and more efficient encryption methods than OpenVPN, but also can be self hosted.
By default you sign up for a Tailscale account (free) and then create your VPN on their servers, sending invites to each client/device to join your VPN, kinda like the older Hamachi days with LogMeIn.
The VPN works beautifully and setup couldn't be more of a breeze.
I created an LXC container with almost no resources just to host a Tailscale instance to allow connections into my homelab via my phone and other devices outside my network without having to expose any services or open any ports.
I want to self host the VPN controller though, so that if Tailscale's website gets breached, or it goes down, I would remain unaffected.
One of the primary goals for a lot of homelabbers is to take control of their data, which is also my goal.

Tailscale LXC creation.
Tailscale installation.

Headscale LXC creation.
Headscale installation.

Headscale has no UI, uses CLI.  Not a deal breaker, but webUI's are the defacto standard for most self hosted services.
Hopefully this will become integrated to Headscale in the future, but for now there are a few options that I've come across.
Headscale-UI from GuruComputing - basic, but only has documentation for Docker.  I don't do Docker.
Headplane from Tale - Runs on NodeJS, good feature list, but I couldn't get this to work
Headscale Admin from GoodiesHQ - Good feature list, UI looks good, but favors Docker.  I tried to get this to work without Docker, but no luck as yet.
Ouroboros from Yellowsink - didn't bother with this
Headscale-UI from Simicu - Could try this
HeadscaleUI from JPHermans - Good UI, written in Python, got this working after some derping around

Show documentation from Obsidian