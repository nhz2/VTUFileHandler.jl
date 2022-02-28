---
title: 'VTUFileHandler: A VTU library in the Julia language that implements an algebra for basic mathematical operations on VTU data'
tags:
  - Julia
  - VTK unstructered grid
  - Stochastic/parametric post-processing of simulation results
authors:
  - name: Maximilian Bittens
    orcid: 0000-0001-9954-294X
    affiliation: "1"
affiliations:
 - name: Federal Institute for Geosciences and Natural Resources (BGR)
   index: 1
date: 28 February 2022
bibliography: paper.bib
---

# Abstract

With increasing computing resources, the investigation of uncertainties in simulation results is becoming an increasingly important factor. To analyze those effects, a discrete numerical simulation is computed several times with different realizations of the input parameters to produce different outputs of the same model. The relevant stochastic or parametric output variables, such as mean value, expected value and variance, are often calculated and visualized only at selected individual points of the whole domain. This project aims to provide a simple way to perform stochastic/parametric post-processing of numerical simulations on the entire domain, here using the VTK unstructed grid (VTU) file system and the julia language as an example.

# Introduction

Consider a discrete computational model $\mathcal{M}$, providing an output-vector $\mathbf{Y}$ for a given set of inputs $\mathbf{X}$:
\begin{equation}\label{eq:discr}
\mathbf{Y} = \mathcal{M}(\mathbf{X})\;.
\end{equation}
The output $\mathbf{Y}$ can be a scalar, a vector, a matrix, or a finite-element post-processing result, for example. In this case, we consider the output to be a VTU file. The input parameters are considers to be a set of scalars $\mathbf{X}= \{X_1,...,X_N\}$, and for simplicity, the set is reduced to a \textit{singleton} ($N=1$). Equation (\ref{eq:discr}) is called the \textit{deterministic case}. As a next step, we introduce a parametric variation $X:=X(\boldsymbol{\xi})$, where $\xi$ maps the input from a minimum to a maximum value. Then we refer to as parametric (or if $\xi$ is a random variable with a propability density function, stochastic ) case:
\begin{equation}\label{eq:stoch}
\mathbf{Y}(\xi) = \mathcal{M}(\mathbf{X}(\boldsymbol{\xi}))\;.
\end{equation}
Since $\mathbf{Y}(\boldsymbol{\xi})$ is no longer deterministic, further methods are required to discretize the \textit{sample space} and to post-process and visualize the results. Different methods for uncertainty quantification can be found in @gates2015multilevel or @sudret2017surrogate, for example.
The most prominent method for computing the expected value of the problem described in Equation (\ref{eq:stoch}) is the Monte-Carlo method:
\begin{equation}\label{eq:montecarlo}
\mathbb{E}[\mathbf{Y}(\boldsymbol{\xi})] \approx \tilde{\mathbb{E}}[\mathcal{M}(\mathbf{X}(\boldsymbol{\xi}))] = \frac{1}{M} \sum\limits_{i=1}^M \mathcal{M}(\mathbf{X}(\xi_i))\,,\quad
\xi_i \sim \mathcal{U}(0,1)\,.
\end{equation} 
From (\ref{eq:montecarlo}) we can conlcude that if $\mathbf{Y}(\xi_i)=\mathcal{M}(\mathbf{X}(\boldsymbol{\xi}))$ is a deterministic VTU result file at position $\xi_i$ in the sample space, it is sufficient to implement the operators `+(VTU-file,VTU-file)` and `/(VTU-file,Number)` to compute the expected value on the whole domain by help of the Monte-Carlo method.


# Features



# References