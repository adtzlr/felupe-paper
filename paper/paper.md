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
FElupe is a Python package for finite element analysis focusing on the formulation and numerical solution of nonlinear problems in continuum mechanics of solid bodies. This package is intended for scientific research, but is also suitable for running nonlinear simulations in general. In addition to the transformation of general weak forms into sparse vectors and matrices, FElupe provides an efficient high-level abstraction layer for the simulation of the deformation of solid bodies.

## Highlights
- 100% Python package built with NumPy and SciPy
- easy to learn and productive high-level API
- nonlinear deformation of solid bodies
- interactive views on meshes, fields and solid bodies (using PyVista)
- typical finite elements
- cartesian, axisymmetric, plane strain and mixed fields
- hyperelastic material models
- strain energy density functions with automatic differentiation

The essential high-level parts of solving problems with FElupe contain a mesh, a numeric region, one or more fields, a constitutive material formulation, a solid body, a dict of boundary conditions, a step and a job. For example, consider a quarter model of a solid cube with hyperelastic material behaviour subjected to a uniaxial elongation applied at a clamped end-face. First, a meshed cube out of hexahedron cells is created. A numeric region, pre-defined for hexahedrons, is created on the mesh. A vector-valued displacement field is initiated on the region and is further added to a field container. A uniaxial load case is applied on the displacement field and creates the boundary conditions. This involves setting up symmetry planes as well as the absolute value of the prescribed displacement at the mesh-points on the right-end face of the cube. The right-end face is clamped, i.e. its displacements, except the components in longitudinal direction, are fixed. An isotropic hyperelastic Neo-Hookean material formulation is applied on the displacement field of a solid body. A step generates the consecutive substep-movements of a given boundary condition. The step is further added to a list of steps of a job. During evaluation, each substep of each step is solved by Newton's method and the field values are updated in-place. Finally, the maximum principal values of logarithmic strain of the last completed substep are plotted.

```python
import felupe as fem

region = fem.RegionHexahedron(mesh=fem.Cube(n=6))
field = fem.FieldContainer([fem.Field(region, dim=3)])
solid = fem.SolidBody(umat=fem.NeoHooke(mu=1, bulk=2), field=field)
boundaries, loadcase = fem.dof.uniaxial(field, clamped=True)

move = fem.math.linsteps([0, 1], num=5)
step = fem.Step([solid], ramp={boundaries["move"]: move}, boundaries=boundaries)
job = fem.Job(steps=[step]).evaluate()

solid.plot("Principal Values of Logarithmic Strain").show()
```

Any other hyperelastic material model formulation may be used instead of the Neo-Hookean material model, most easily by its strain energy density function. All built-in hyperelastic material models provide a plot-method to visualize force-stretch curves for the homogeneous load cases uniaxial and equi-biaxial tension as well as planar shear.

# Examples
The documentation of FElupe contains many interactive tutorials and examples. Resulting deformed solid bodies of some of these examples are shown in Fig. 1. Several scientific publications include computational results of FElupe, e.g. XX, YY.

# References
