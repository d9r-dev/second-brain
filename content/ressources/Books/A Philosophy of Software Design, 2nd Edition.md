---
title: A Philosophy of Software Design, 2nd Edition
draft: false
publish: true
tags:
  - 📬
  - software-development
  - software-design
date: 2025-06-20
---
Date: Juli 2021
Author: [John Ousterhout](https://www.amazon.de/John-Ousterhout/e/B000APICQY/ref=dp_byline_cont_book_1) 

## 1: Introduction

There are two general approaches to fighting complexity, both of which will be discussed in this book. The first approach is to eliminate complexity by making code simpler and more obvious. For example, complexity can be reduced by eliminating special cases or using identifiers in a consistent fashion. The second approach to complexity is to encapsulate it, so that programmers can work on a system without being exposed to all of its complexity at once. This approach is called modular design. 

### 2.1 Complexity defined

Complexity is anything related to the structure of a software system that makes it hard to understand and modify the system.

### 2.2 Symptoms of complexity

Complexity is more apparent to readers than writers. If you write a piece of code and it seems simple to you, but other people think it is complex, then it is complex.

### 2.1 Complexity defined

overall complexity of a system (C) is determined by the complexity of each part p (cp) weighted by the fraction of time developers spend working on that part (tp). Isolating complexity

### 2.2 Symptoms of complexity

Change amplification: The first symptom of complexity is that a seemingly simple change requires code modifications in many different places.

Cognitive load: The second symptom of complexity is cognitive load, which refers to how much a developer needs to know in order to complete a task

Sometimes an approach that requires more lines of code is actually simpler, because it reduces cognitive load.

Unknown unknowns: The third symptom of complexity is that it is not obvious which pieces of code must be modified to complete a task, or what information a developer must have to carry out the task successfully

### 2.3 Causes of complexity

One of the most important goals of good design is for a system to be obvious.

obscurity

dependencies

For the purposes of this book, a dependency exists when a given piece of code cannot be understood and modified in isolation; the code relates in some way to other code, and the other code must be considered and/or modified if the given code is changed.

Obscurity occurs when important information is not obvious.

### 3.2 Strategic programming

The first step towards becoming a good software designer is to realize that working code isn’t enough. It’s not acceptable to introduce unnecessary complexities in order to finish your current task faster. The most important thing is the long-term structure of the system. Most of the code in any system is written by extending the existing code base, so your most important job as a developer is to facilitate those future extensions. Thus, you should not think of “working code” as your primary goal, though of course your code must work. Your primary goal must be to produce a great design, which also happens to work. This is strategic programming.

### 4.1 Modular design

modular design, a software system is decomposed into a collection of modules that are relatively independent. Modules can take many forms, such as classes, subsystems, or services. In an ideal world, each module would be completely independent of the others: a developer could work in any of the modules without knowing anything about any of the other modules. In this world, the complexity of a system would be the complexity of its worst module.

### 4.1 Modular design

an interface and an implementation. The interface consists of everything that a developer working in a different module must know in order to use the given module. Typically, the interface describes what the module does but not how it does it.

### 4.2 What’s in an interface?

The interface to a module contains two kinds of information: formal and informal. The formal parts of an interface are specified explicitly in the code, and some of these can be checked for correctness by the programming language.

### 4.3 Abstractions

The informal parts of an interface include its high-level behavior, such as the fact that a function deletes the file named by one of its arguments.

The informal aspects of an interface can only be described using comments, and the programming language cannot ensure that the description is complete or accurate

An abstraction is a simplified view of an entity, which omits unimportant details

An abstraction can go wrong in two ways. First, it can include details that are not really important; when this happens, it makes the abstraction more complicated than necessary, which increases the cognitive load on developers using the abstraction. The second error is when an abstraction omits details that really are important. This results in obscurity: developers looking only at the abstraction will not have all the information they need to use the abstraction correctly

4.4 Deep modules

The best modules are those that provide powerful functionality yet have simple interfaces. I use the term deep to describe such modules.

4.6 Classitis

shallow module is one whose interface is complicated relative to the functionality it provides. Shallow modules don’t help much in the battle against complexity, because the benefit they provide (not having to learn about how they work internally) is negated by the cost of learning and using their interfaces. Small modules tend to be shallow.

4.7 Examples: Java and Unix I/O

Classitis may result in classes that are individually simple, but it increases the complexity of the overall system. 

5.1 Information hiding

The basic idea is that each module should encapsulate a few pieces of knowledge, which represent design decisions. The knowledge is embedded in the module’s implementation but does not appear in its interface, so it is not visible to other