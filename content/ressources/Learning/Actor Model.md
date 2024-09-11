---
title: Actor Model
draft: false
publish: true
tags:
  - design-patterns
  - software-architecture
date: 2024-09-02
---
References: [[Software Architecture]] [[Design Patterns]]

- Conceptual model of concurrent computation from 1973
- Actor is a fundamental unit of computation
	- allowed operations of an actor are:
		- Create another actor
		- send a message
		- designate how to handle the next message
	- holds his own private state
	- actors are isolated by each other and don't share memory
	- state of the actor can only changed by messages
	- messages are send to actors and are handled in FIFO (First In First Out) order
	- messages are simple, immutable data structures
	- actors work asynchronously and have addresses
	- an actor holds the addresses of actors he himself created
	- an actor can contain addressees from messages he receives
	- actor can have different addressees, address != identity
	- an actor can supervise other child actors he creates
	- a supervisor can check if other actors are live and redirect messages
	- leads to self healing systems
- pros:
	- easy to scale
	- geographical distribution
	- fault tolerance
	- no shared state
- cons:
	- actors susceptible to deadlocks
	- actors mailbox overflowing
- Implementations: akka, Elixir, Erlang