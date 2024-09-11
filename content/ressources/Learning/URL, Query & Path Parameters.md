---
title: URL, Query & Path Parameters
draft: false
publish: false
tags:
  - 🌻
  - API-Design
date: 2024-09-09
---
## The difference between a path variable and a query parameter

![[Pasted image 20240909124656.png]]
![[Pasted image 20240909124706.png]]
Imagine you have a jar full of balls with different colors. Each of this balls represents a item in our database with an ID and a color. If you want to get all the balls with the same color you would use a query parameter. Think of the query parameter as a kind of filter. 

Example: `/balls?color=yellow`

But let's say you want to fetch a very specific ball out of the jar (your database). For a [[REST]]ful-API it is the best practice to use a path variable. 

Example: `/ball/{ballId}`

More Ressources:
[Swagger on Describing Parameters](https://swagger.io/docs/specification/describing-parameters/)

