---
title: Serverless Architecture
draft: false
publish: true
tags:
  - software-architecture
  - serverless
date: 2024-09-02
---
- [Introduction](https://martinfowler.com/articles/serverless.html)
- application designs that incorporate Backend as a Service (BaaS) from third parties or run on Functions as a Service platforms (FaaS)
- in combination with Single-Page-Applications they remove the need for a always on server component
- FaaS -> developer still writes backend code, but it is run on a ephemeral (may only last one invocation) event-triggered, stateless compute containers fully run by third party providers like AWS, Google or Microsoft
- emphasis on choreography over orchestration
- more flexible and amenable to change, easier to upgrade, better division of concerns, cost benefits
- requires better distributed monitoring, relieant on the security capabilities of the vendor
- FaaS have start up time and so called cold starts -> Server for the function has to be spun up, impact depends on kind of function
- You have a limit on the run time of a function and they must be stateless
- a API-Gateway is a HTTP Server that routes the requests to the needed function service

References: [[Software Architecture]]