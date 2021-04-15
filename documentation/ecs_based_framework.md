---
title: Brainstorming modelling framework
subtitle: 
author: 
  - Mossa
theme: metropolis
institute: IVH
aspectratio: 1610
date: 2021-04-15
linkcolor: red
urlcolor: CornflowerBlue
header-includes:
    # - \RequirePackage{fira} # you've got to install this before the font works
    - \usepackage{fontspec}
    - \setmonofont[Contextuals={Alternate}]{Fira Code}
    - \makeatletter
    - \def\verbatim@nolig@list{}
    - \makeatother
---

<!-- markdownlint-disable-file MD025 -->

## Background

It is easier to constraint opinions, when it has to fit within the frames of
a Beamer-presentation.

Other documents to read first:

* [Model Framework Project](documentation/Model%20Framework%20Project%20v5.md)
* [Model Requirement Sheet](documentation/Model%20Requirement%20Sheet%20v4.md)

### Approach here

We decided to take a **top-down** design approach, thus we'll start by listing
a general overview and then cut down further.

## Overview

Coupling between R and *compiled language[^compiled_lang]*: There must be
a way to define code in R and have that code run in the **compiled language**.

This means that every requirement we are able to formulate within a compiled language
has to be to be setup and piped through the compiled language.

[^compiled_lang]: Rust/Fortran/C/C++.

## General process modules in the framework

These are:

- Population
- Disease Model
- Regulator / Authorities

Stored state within these models should comply with the interface

## Latency between R and Rust

* Serialization/Deserialization between R & Rust is a way to start the process,
  but is not a sustainable solution forward. Pointers has to be passed back and
  forth.

* Provide what is allowed to be changed from the R-side, thus we can ensure that
  costly inquiries to the *population* can be facilitated through the Rust.

* [ ] Is it possible to JIT-compile R code that then can be embedded in Rust
  and figure into the compilation.

# Storage

During simulation, actually storing the model state in a hierarchical data
structure is not a good idea. Instead, we should aim for cache-friendly
organisation of the data.

This is where an ECS comes in.

However, there is a storage component that have to be considered, where the trade-off
is between faster insertion/deletion of new entities, or updating existing entities.

# Recording

