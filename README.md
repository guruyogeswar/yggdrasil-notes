# Yggdrasil

A simulation exploring whether persistent internal state, memory decay, and social consequence can produce stable long-term agent behavior in virtual worlds—without explicit reward optimization or scripting.

---

## What this project is

Yggdrasil is an ongoing experiment, not a finished product.

The central question: **What happens when agents must acquire energy to survive, and nothing else is specified?**

The simulation places agents in a virtual world where every computation has a metabolic cost. Agents that run out of energy die. Agents that accumulate enough energy can reproduce. There are no programmed behaviors, no reward functions, no fitness objectives—only the physics of energy.

Layered on top of this constraint is a set of cognitive mechanisms: systems for forming memories, for decaying old information, for modeling what other agents might do. The goal is not to build intelligent agents, but to see what patterns emerge when simple survival pressure meets structured information processing.

I don't know what this architecture can or cannot produce. I am studying it.

---

## Why I started this

I kept running into the same problem in reinforcement learning: the "intelligence" was always hiding in the reward function. Agents would do impressive things, but only because someone had carefully engineered exactly what "good" meant. Change the reward slightly and the behavior collapsed.

Scripted game AI had the opposite problem—robust but brittle. Every behavior was hand-authored. The agents couldn't surprise you because there was nothing to discover.

I wanted to see what would happen if I removed both crutches. No reward signal to optimize. No behavior trees to follow. Just energy conservation and the problem of staying alive long enough to reproduce.

It seemed plausible that interesting behaviors might emerge from this constraint alone. The thermodynamic framing appealed to me because it felt like a genuine constraint rather than a designed objective.

---

## How the system works (at a high level)

Each agent maintains continuous internal state: energy reserves, drive levels (hunger, fatigue, social need), and an array of chemical signals that modulate processing.

Every tick, agents perceive their local environment, update their internal drives, and select an action. Actions have metabolic costs. Eating restores energy. Moving depletes it. Thinking depletes it too—there is no free computation.

Memory works through a simple encoding/retrieval loop. Experiences are stored as {context, action, outcome} tuples. When an agent encounters a similar context, relevant memories surface and influence action selection. Memories decay if not reinforced.

Agents can observe each other's actions. When agent A watches agent B do something that leads to a good outcome, A can update its own action preferences. This creates a channel for social learning that I did not explicitly program—it falls out of the memory and observation systems interacting.

There is a mechanism for agents to emit signals—abstract vectors, not words. Whether these signals develop stable meaning depends on whether coordinated behavior proves useful for survival. In some runs, signal conventions emerge. In others, they don't.

---

## One concrete behavior I observed

In runs with resource scarcity, I noticed something I did not expect.

Agents that had discovered a reliable food patch would sometimes emit signals before eating. Other agents would approach. The original agent would leave. The approaching agents would find food.

I initially interpreted this as teaching or cooperation. But watching more carefully, I'm not sure that's right. It might be simpler: the signaling agent had already eaten, was no longer hungry, and the signal was just a side effect of some internal state change that happened to correlate with food presence.

The approaching agents learned to associate that signal pattern with food locations—but whether the original agent "intended" to communicate is unclear.

This kind of ambiguity happens a lot. Patterns that look purposeful often have simpler explanations. I'm still trying to develop better methods for distinguishing genuine coordination from coincidental correlation.

---

## What failed or surprised me

The most consistent failure mode is what I call "the expensive brain problem."

In environments where food is abundant and nothing much changes, agents with active higher cognition—planning, mental modeling of others—actually survive *worse* than agents without these systems. The metabolic cost of thinking exceeds the survival benefit.

This shouldn't have surprised me, but it did. I had implicitly assumed that more cognitive capability would always help. It doesn't. In stable environments, cognition is overhead.

The systems only prove their value when the environment becomes unpredictable—when resources shift location, when other agents become competitive rather than irrelevant, when the rules change mid-simulation. Then the planning-capable agents adapt while the simpler agents die.

I don't have a clean solution for this. The architecture correctly reflects a real tradeoff: intelligence is expensive. Whether that's a feature or a bug depends on what question you're asking.

---

## What I am exploring next

I'm trying to understand what minimal environmental complexity is required to make social cognition net-positive.

Right now, the environments I test in are probably too simple. Agents with Theory of Mind show as metabolic overhead because there's nothing socially complex enough to require mental modeling. If I add competitive dynamics—resource guarding, deception, coalition formation—will these systems start paying for themselves?

The broader question: is there a phase transition where cognitive complexity suddenly becomes essential, or is it a smooth gradient?

I don't have a roadmap. I'm running experiments.

---

## Technical notes

The simulation is written in C++ and runs at approximately 300 ticks per second with 100 agents. All memory is pre-allocated—no runtime allocation, which makes performance predictable.

Any cognitive system can be disabled via command line flag (`--ablate hippocampus`, `--ablate tom`, etc.). This is not for debugging—it's for running controlled experiments to isolate the contribution of individual mechanisms.

The code is research-grade. It works, but it prioritizes scientific utility over polish.

---

## Contact

Guru Yogeswar Reddy  
guruyogeswar@gmail.com
