---
title: "dg-solvax"
date: 2026-09-06
draft: false
summary: "Discontinuous Galerkin and Riemann solver in JAX."
topics: ["Physics", "AI", "Open Source Software"]
tags: ["Boltzmann-equation", "spintronics", "magnons", "neural-operators", "AI", "oss"]
code: https://github.com/D-A-Reiss/dg-solvax
---

During my research on how to solve the Boltzmann equation, an integro-differential equation which forms the foundation of computational fluid dynamics (CFD), in certain scenarios interesting in spintronics*, I discovered that a discontinuous Galerkin (DG) method might be suited well in order to do so.
Although I haven't finished this research project yet, in the spirit of the incremental approach of software development and as the core functionality might be applicable in other scenarios like producing data for training [neural operators](https://neuraloperator.github.io/dev/index.html), I decided to publish in an open-source [PyPI package](...):
- a solver applying a user-specified DG scheme to (systems of) partial differential equations, using
- a solver to compute numerical fluxes through the finite elements' boundaries via solving the associated Riemann problem.

All in JAX. Built on the basis of [diffrax](https://github.com/patrick-kidger/diffrax). 

See [GitHub](https://github.com/D-A-Reiss/dg-solvax) for more details.

*(while there are a lot of software packages for solving the Boltzmann equation for phonons, there are none for the case of magnons)
