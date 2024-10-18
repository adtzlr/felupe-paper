---
title: 'FElupe: Finite element analysis for continuum mechanics of solid bodies'
tags:
  - python
  - finite-elements
  - hyperelasticity
  - computations-mechanics
  - scientific-computing
authors:
  - name: Andreas Dutzler
    orcid: 0000-0002-9383-9686
    affiliation: [ 1, 2 ]
    corresponding: true
  - name: Martin Leitner
    orcid: 0000-0002-3530-1183
    affiliation: 1
affiliations:
  - index: 1
    name: Institute of Structural Durability and Railway Technology, Graz University of Technology, Austria
  - index: 2
    name: Siemens Mobility Austria GmbH, Austria
date: 18 October 2024
bibliography: paper.bib
---

# Summary
FElupe is a Python 3 finite element analysis package focusing on the formulation and numerical solution of nonlinear problems in continuum mechanics of solid bodies. This package is intended for scientific research, but is also suitable for running nonlinear simulations in general. In addition to the transformation of general weak forms into sparse vectors and matrices, FElupe provides an efficient high-level abstraction layer for the simulation of the deformation of solid bodies.

## Highlights
- 100% Python package built with NumPy and SciPy
- easy to learn and productive high-level API
- nonlinear deformation of solid bodies
- interactive views on meshes, fields and solid bodies (using PyVista)
- typical finite elements
- cartesian, axisymmetric, plane strain and mixed fields
- hyperelastic material models
- strain energy density functions with automatic differentiation

# References
