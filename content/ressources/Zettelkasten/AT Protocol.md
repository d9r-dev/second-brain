---
title: AT Protocoll
draft: false
publish: true
tags:
  - 📬
  - social-media
date: 2025-01-17
---
Open Source Social Media Protocol from Bluesky

## [A Self-Authenticating Social Protocol](https://bsky.social/about/blog/3-6-2022-a-self-authenticating-social-protocol)

Self-authenticated data moves the authority to the user. This data is inherently live - that is, canonical and transactable - no matter where it is located. The Web is connection-centric. That means, when your content is not hosted anywhere anymore it becomes dead.

The three components that enable self-authentication are [[cryptographic identifiers]], [[content-addressed data]], and [[verifiable computation]].

Most important objectives are portability, scale and trust. 

### Portability

Portability is the ability to move between services without losing everything. Now when you want to switch from X to Threads you lose all your posts and your social graph. That is even the case with other federated protocols like [[ActivityPub]] and [[Matrix]]. Self-authenticating protocols allow to switch providers because the authority lies within the data and not within the host.

### Scale

Social networking platforms bring hundred of millions of people together in a global conversation. For this special infrastructure is needed. The challenge is to combine decentralization with scale and keep a global view across the network. Self-authenticating data enable store-and-forward caches. Aggregators can host data on behalf of smaller providers without reducing trust in the data's authenticity. 

### Trust

The algorithms and moderation rules of social media platforms are intransparent. Especially since Elon Musk bought Twitter and turned it into a right wing propaganda machine, but also other networks like Facebook are full of biases and often enough just try to engage their users through polarization. AT Protocol tries to build around trust by exposing what's going on under the hood and allowing users to adjust their experience. Self-authenticated data can retain metadata, like publisher or changes. Verifiable computation provides new tools for establishing trust by showing precisely how the results were produced. 

