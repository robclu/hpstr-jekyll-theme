---
layout: page
title: 
image:
  feature: about.jpg
  credit: WeGraphics
  creditlink: http://wegraphics.net/downloads/free-ultimate-blurred-background-pack/
comments: false
modified: 2016-02-01
---

Hello, and welcome to my online blog -- I hope you find something useful here :)

I'm Rob, and I enjoy programming. I mostly write C++ code, and what I find most interesting is concurrency (shared memory programming, interprocessses, and massive parallelism), graphics, optimisation, and physics. I also like python, although I don't really have an advanced enough knowledge to provide an accurate
commentary on it, so it's unlikely many blog posts will be python related. This may change in the future though.

I'm currently doing an MPhil in Scientific Computing at the University of
Cambridge, where I'm looking at using GPUs to accelerate multi-physics problems.

I try to constantly keep learning, and to work on personal projects which explore the new things I learn. I think that writing about something is a good way to test your understanding, and it's always nice to have a reference to go back to at a later stage.

Recently, I've started storing my project related work in a central place, so
most of my recent work can be found at the [Voxel repository](https://github.com/Voxelated), for which the documentation is at [Voxel documentation](https://voxelated.github.io/index.html). My [GitHub repository](https://github.com/robclu) also has some code samples, although most of what I do is no longer stored there. The most notable non-academic projects are:

## Non-Academic Projects

* __Voxel:__ This is a general purpose utility library that I use throughout
  other projects. Some of the notable features are general GPU invokable Lambda, some heterogeneous classes (CPU and GPU support, like Tuple for example), threading utility, and system information for large system configurations. You can browse the [repository](https://github.com/Voxelated/Voxel) or the [documentation](https://voxelated.github.io/libraries/voxel/index.html)

* __Conky:__ This is a concurrency and parallelism library. It contains
  concurrent data structures and high-level abstractions which allow large-scale
  distributed and massively parallel code to be written, simply. It's a work in
  progress, but you can check out the [repository](https://github.com/Voxelated/Conky) or the [documentation](https://voxelated.github.io/libraries/conky/index.html)

* __Xpress:__ An expression template library which allows numpy like array
  creation and operations in C++, which are accelerated on the GPU if the system
  supports the GPU, or many-core systems if there is support for that. See the
  [repository](https://github.com/Voxelated/Xpress).


## Academic Projects

* ___```Parahaplo:```___ A parallel implementation of the minimum 
  error-correction individual haplotype assembly problem -- an NP-hard problem
  -- using a parallel graph search executed on the GPU. The project in its current (not updated) implementation can achieved a 50x performance. The accuracy is slightly less than the best solutions in existing research. I'm sure that the cause of the rediced accuracy is a software bug, and will hopefully fix it when I get a chance. The codebase also needs to be 
  refactored, which I'll hopefully get a chance to do eventually. Here is the
  [repository](https://github.com/robclu/parahaplo), as well as the [paper](https://github.com/robclu/parahaplo/blob/master/doc/Parahaplo.pdf).

## Publications

The following is a list of papers I have written (hopefully this will grow):

R. Clucas and S. Levitt, CAPP: A C++ Aspect-Oriented Based Framework for Parallel Programming with OpenCL, in Proceedings of the 2015 Annual Research Conference on South African Institute of Computer Scientists and Information Technologists, ser. SAICSIT 15. New York, NY, USA: ACM, 2015, pp. 10:110:10. [Online]. Available: [http://doi.acm.org/10.1145/2815782.2815818](http://doi.acm.org/10.1145/2815782.2815818) [Camera ready draft- [[1]](https://github.com/robclu/capp/blob/master/documentation/final_version/Capp.pdf)]

[1] : [https://github.com/robclu/capp/blob/master/documentation/final_version/Capp.pdf](https://github.com/robclu/capp/blob/master/documentation/final_version/Capp.pdf)  