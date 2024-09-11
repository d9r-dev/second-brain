---
title: How to conquer fear in development
draft: true
publish: false
tags:
  - 🌱
date: 2024-09-10
---
Once I had a colleague who hated it to do deployments on the production systems. She said: "What if something goes wrong? I don't really know what to do then." Of course it is a bad feeling to deploy a production system for a client with fear in your mind. But how comes there was so much fear involved?

Well the answer is pretty easy: The only tests that were run before a deployment were manual tests and some E2E-Tests. There were zero unit tests and or integration tests. Why not? Well, first of all, the company culture at least in some teams did not really support extensive testing. But also the client was not really interested in paying for more extensive testing. They just did not see the business value of testing, and the developers were ready to play along, because they did not really see the value of tests themselves, only that they had to write more code. 

But as you can imagine the fear before a deployment would be much less if you had run an comprehensive test suite and saw all the green check marks in the reports lighting up. 