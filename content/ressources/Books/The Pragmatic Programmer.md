---
title: The Pragmatic Programmer
draft: false
publish: false
tags:
  - 📬
  - 📖
  - programming
  - software-development
  - advice
date: 2024-11-04
---
Author: David Thomas, Andrew Hunt

## Summary

## Quotes

2 "As Martin Fowler says "you can change your organization or you can change your organization"."

### Take Responsibility

4 "... but it is up to you to provide solutions, not excuses."

"Tip 4 Provide Options, Don't Make Lame Excuses"

5 "When you find yourself saying, "I don't know." be sure to follow it up with " - but I'll find out." It's a great way to admit what you don't know, but then take responsibility like a pro."

### Software Entropy

6 Broken window effect in cities. One broken window in a building that is left unrepaired for a longer time creates a sense of abandonment and leads to littering. 

[[Contagious Depression]]

7 "Tip 5: Don't Live with Broken Windows"

## The Essence of Good Design

28 
"Tip 14: Good Design Is Easier to Change Than Bad Design"
ETC principle: Easy to Change
29
"try to make your code replaceable"
31
"Every piece of knowledge must have a single, unambiguous, authoritative representation within a system."

Tip 15: DRY - Don't Repeat Yourself
"Dry is about duplication of *knowledge*, of *intent*. It's about expressing the same thing in two different places, possibly in two totally different ways."

## Orthogonality

39 "In a well-designed system, the database code will be orthogonal to the user interface: you can change the interface without affecting the database, and swap databases without changing the interface."

40f "Tip 17 Eliminate Effects Between Unrelated Things"

"We want to design components that are self-contained: independent, and with a single, well-defined purpose (...cohesion)"

### Gain Productivity
- Changes are localized
- promotes reuse 
- more functionality as when components overlap

### Reduce Risk
- Diseased sections of code are isolated
- The resulting system is less fragile
- better tested
- no vendor or platform lock

42 Layered Design

"There is an easy test for orthogonal design. Once you have your components mapped out, ask yourself: If I dramatically change the requirements behind a particular function, how many modules are affected? In an orthogonal system, the answer should be "one.""

51 
"Tip 20 Use Tracer Bullets to Find he Target"

Tracer bullets are put in between regular ammo to see where you are shooting at. 

"Like the gunners, you're trying to hit a target in the dark. Because your users have never seen a system like this before, their requirements may be vague. Because you may be using algorithms, techniques, languages, or libraries you aren't familiar with, you face a large number of unknowns. And because projects take time to complete, you can pretty much guarantee the environment you're working in will change before you're done."

52f. 

Develop a path from end-to-end of your application with the most important requirements and unknowns first. Did you hit the target?

57 "Tip 21 Prototype to Learn"

61
> Why Don't Many Business Users Read Cucumber Features?
> 
> One of the reasons that classic gather requirements, design, code, ship approach doesn't work is that it is anchored by the concept that we know what the requirements are. But we rarely do. Your business users will have a vague idea of what they want to achieve, but they neither know nor care about the details. That's part of our value: we intuit intent and convert it to code.
> 
> So when you force a business person to sign off on a requirements document, or get them to agree to a set of Cucumber features, you're doing the equivalent of getting them to check the spelling in an essay written in Sumerian. They'll make some random changes to save face and sign it off to get you out of their office.
> 
> Give them code that runs, however, and they can play with it. That's where their real needs will surface.

66 Estimating

Choose the units of your answer to reflect the accuracy you intend to convey.

- 1-15 days Days
- 3-6 weeks Weeks
- 8-20 weeks Months
- 20+ weeks Think hard before giving an estimate
- e.g. 25+ weeks 6 Months

trick that always gives good answers: ask someone who's already done it.

66

#### Understand What's Being asked

you need to have a grasp of the domain.

#### Build a Model of the System

The parts of the problem or architecture. What needs to be done.

#### Break the Model into Components

How does each component contribute mathematically to the estimation?

#### Give Each Parameter a Value

To give it a value compare it to known values. Parameters to add are less important than parameters to multiply.

### Calculate the Answers

Calculate the answer in a range of possible outcomes. 

70 
How do you eat an elephant? One bite at a time.
"Tip 24 Iterate the Schedule with the Code"

repeating the following steps with every thin slice of functionality:

- Check requirements
- Analyze risk (and prioritize riskiest items earlier)
- Design, implement, integrate
- Validate with the users

What to Say When Asked for an Estimate --> "I'll get back to you."

75 
"Tip 25 Keep Knowledge in Plain Text"