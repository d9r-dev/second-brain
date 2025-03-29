---
title: Why I'm No Longer Talking to Architects About Microservices
draft: false
publish: true
tags:
  - 📖
  - microservices
  - software-architecture
date: 2025-03-25
---
[Source](https://blog.container-solutions.com/why-im-no-longer-talking-to-architects-about-microservices)

In this piece, Ian Miell explains why he's become frustrated with discussions about [[microservices]] among architects. He outlines three main problems:

1. Lack of a Clear Definition: There's no consensus on what constitutes a microservice. Different experts define it variously - from lines of code to team size to autonomous processes. This definitional ambiguity leads to unproductive conversations where people are essentially talking past each other.
2. Disconnection from Business: Goals Microservices discussions often become abstract and detached from concrete business problems. People frequently cite vague benefits like improved scalability or agility without explaining specific improvements. Miell argues that most organizations would be better off maintaining a well-structured monolith until they have a compelling reason to switch.
3. Organizational Challenges: Implementing microservices isn't just a technical challenge - it requires significant organizational changes. This includes creating cross-functional autonomous teams, decentralizing decision-making, and developing a mature DevOps culture. Without these structural changes, microservices will likely increase complexity without delivering real benefits.

Miell suggests moving away from debating microservices and instead focusing on practical goals like reducing cycle time, improving reliability, and solving specific business bottlenecks. He believes that if breaking a system into smaller services genuinely helps achieve these objectives, then that approach makes sense.

The article concludes by highlighting the difficulty of organizational transformation, noting that changing business structures is far more challenging than modifying software architecture, especially in larger organizations.

Here are the most important quotes from the article:

1. On the lack of microservices definition: "If a term causes this much confusion, maybe it's outlived its usefulness."
2. On the disconnect from business goals: "Start talking about reducing cycle time, improving reliability, and solving concrete business bottlenecks. If breaking up a system into smaller services is the best way to achieve those outcomes, fine, but angels on a pinhead discussions among architects about microservices are not the way to get there."
3. On organizational challenges: "Microservices don't work in a vacuum. They require teams to be structured in a way that supports them."
4. On the core problem with microservices discussions: "Instead of arguing about what to call our architecture, we could be talking about concrete challenges, or specific trade-offs: how to deploy new features faster, how to reduce coupling, how to scale parts of the system."
5. On the evolution of technical terms: "Each started with a well-defined intent, but over time they've been stretched and contorted to mean whatever the speaker wants to advocate or criticise."
6. A key warning about microservices adoption: "Sam Newman, author of Building Microservices, frequently warns that most organizations should not start with microservices unless they have a compelling reason."
7. On the fundamental principle: "Tech should follow business needs, not the other way around."