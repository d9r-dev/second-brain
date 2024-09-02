---
title: Amdahl's Law
draft: false
publish: true
tags:
  - computer-science
  - performance
date: 2024-09-02
---
References: [[Computer Science]] [[Performance]]

The main idea is that when we speed up one part of a system, the effect on the overall system performance depends on both how significant this part was and how much it sped up. Consider a system in which executing some application requires time Told. Suppose some part of the system requires a fraction α of this time, and that we improve its performance by a factor of k. That is, the component originally required time αTold, and it now requires time (αTold)/k.

The overall execution time would thus be

Tnew=(1−α)Told+(αTold)/k=Told[(1−α)+α/k]

From this, we can compute the speedup S = Told/Tnew as

S=1(1−α)+α/k

As an example, consider the case where a part of the system that initially consumed 60% of the time (α = 0.6) is sped up by a factor of 3 (k = 3). Then we get a speedup of 1/[0.4 + 0.6/3] = 1.67×.