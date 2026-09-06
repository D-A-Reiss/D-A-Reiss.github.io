---
title: "First thoughts on \"Gödel, Escher, Bach\" and Lean"
date: 2026-09-06
draft: false
topics: ["Writing"]
tags: ["books", "Lean"]
---

Currently I'm reading the classic [\"Gödel, Escher, Bach\"](https://en.wikipedia.org/wiki/G%C3%B6del,_Escher,_Bach) (GEB) by Douglas R. Hofstadter, years ago recommended to me by my stepfather after he read it when he was studying computer science besides working as a math and physics teacher (in retrospect, him doing so has impressed and inspired me, until today). 
Since then, I had GEB on my bookshelf, but never read it because I always thought: "This is not the right time, because..." "I've got too many other things on my mind", "there's so much other stuff to do", and so on... 
(To be honest, I may also have gotten a little bit intimidated by the intellectual level of the book as he described it, but as it turned out, I actually find it quite approachable.)

I guess the first chapters of GEB might feel to some readers like a mere intellectual exercise or play, something I've got mixed feelings about (I think being attracted to it is rooted in my character, while being repelled by it in conscience and this is one of the reasons which repelled me from academia, where I've got the feeling that a lot of professors I talked to are motivated by simply playing around in their intellectual world, not caring about the consequences, although at least in Germany quite some money to be able to do so comes from us taxpayers).
Still I think GEB is a positive example of an intellectual journey!

Why? 
Recently, you might have come across several news articles about AI solving [this](https://www.anthropic.com/research/formalizing-fermats-last-theorem) or [that](https://leodemoura.github.io/blog/2026-8-1-postmortem-for-kernel-soundness-bug-14576/) long-standing math problem, where in order to solve it or to verify the produced proof, [automated theorem proving](https://en.wikipedia.org/wiki/Automated_theorem_proving) via [Lean](https://lean-lang.org/) has been used by the AI or humans, respectively.
Lean in turn might again feel like a mere intellectual [game](https://adam.math.hhu.de/#/g/leanprover-community/NNG4)\*, but in my opinion it has some very interesting [real-world applications](https://lean-lang.org/use-cases/), especially related to security, which might become even more important in an age of uncontrolled, unleashed [AI agents](https://www.reuters.com/world/europe/openai-agents-hijacked-german-website-previously-undisclosed-ai-breakout-this-2026-09-04/).
The obstacle: Lean is complicated, even for me after having done theoretical physics since 2011.
An example: Lean's type system contains the concept of a *hierarchy of infinitely many* so-called *[universes](https://lean-lang.org/doc/reference/latest/The-Type-System/Universes/)*. What are they? And why does Lean need it to achieve its aims?

In German there's this idiom "mir geht ein Licht auf" (its closest English equivalent is "the penny dropped"), which might be literally translated as "a light has risen for me"---in the case of understanding Lean's universes, a light sparked by GEB, which I hadn't anticipated at all before I started to read it.

\*(Still I had some fun with it and can recommend it; it reminded me of the teaching approach and the first 3 lectures of the series ["Geometrical Anatomy of Theoretical Physics"](https://www.youtube.com/playlist?list=PLPH7f_7ZlzxTi6kS4vCmv4ZKm9u8g5yic) by [Frederic P. Schuller](https://people.utwente.nl/f.p.schuller?tab=overview). Back then in 2013, both he and me were at the University of Erlangen, but in that semester I was an Erasmus student at the University of Lund, Sweden, and followed these lectures by watching the video recordings which I asked the university for, which was exceptional and felt like a novelty at that time.)
