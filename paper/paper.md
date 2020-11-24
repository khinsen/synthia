---
title: 'Synthia: multidimensional synthetic data generation in Python'
tags:
  - synthetic-data
  - copula
  - fpca
  - machine-learning
  - data-science
  - python
authors:
  - name: David Meyer
    orcid: 0000-0002-7071-7547
    affiliation: "1, 2"
  - name: Thomas Nagler
    orcid: 0000-0003-1855-0046
    affiliation: 3
affiliations:
 - name: Department of Meteorology, University of Reading, Reading, UK
   index: 1
 - name: Department of Civil and Environmental Engineering, Imperial College London, London, UK
   index: 2
 - name: Mathematical Institute, Leiden University, Leiden, The Netherlands
   index: 3
date: 22 October 2020
bibliography: paper.bib
---


# Summary

Synthetic data are artificially generated data, not obtainable by direct measurements [@McGraw-Hill-2003]. To serve a similar purpose to real data, synthetically generated data need to preserve the statistical properties of real data in terms of the individual behavior of variables and their (inter-)dependencies. Copula and functional Principle Component Analysis (fPCA) are statistical methods that allow these properties to be simulated [@Joe_2014]. Synthetic data have the potential to augment, or replace, samples in existing datasets. For example, they have been used to augment data for machine learning (ML) applications [@Meyer_et_al], or to replace real data for privacy protection [@Machanavajjhala_2008]. Although several methods of synthetic data generation exist, copulas-based methods have been shown successful for modelling complex interdependencies [@Patki_2016].


# Statement of need

Synthia is an open source Python package that can model univariate and multivariate data, parameterize data using empirical and parametric methods, and manipulate marginal distributions. It supports three different methods of multivariate data generation using fPCA, parametric (Gaussian) copula, and vine copula models for continuous (all), discrete (vine), and categorical (vine) variables. It has a simple and succinct API to natively handle xarray's [@hoyer2017xarray] labelled arrays and datasets (Table 1) in Python. It uses a pure Python implementation for fPCA and Gaussian copula, and relies on the fast and well tested C++ library vinecopulib [@nagler_thomas_2020_4287554] through pyvinecopulib's [@nagler_thomas_2020_4288292] bindings for fast and efficient computation of vines.

Synthia is designed to enable scientists and practitioners to easily fit and generate synthetic data in subjects such as weather and climate and computational sciences where the use of labelled multidimensional data are common. As such, Synthia has been used in @Meyer_et_al to improve the predictions of a ML emulator of atmospheric longwave radiation.

\pagebreak

# Example application

Here we show how to fit and generate multivariate data using Synthia's Gaussian copula and fPCA classes in just three lines of code. We define a reduced dataset of atmospheric temperature profiles (Table 1a) from the EUMETSAT Satellite Application Facility (SAF) on Numerical Weather Prediction (NWP) dataset [@Eresmaa_2014] as the source dataset and fit a Gaussian copula (Table 1b) and fPCA (Table 1c) model to the source dataset to generate 500 new random profiles.

| (a) Source                                    | (b) Synthetic with Gaussian Copula                        | (c) Synthetic with fPCA                           |
| --------------------------------------------- | --------------------------------------------------------- | ------------------------------------------------- |
| `ds = syn.util.load_dataset()`                | `g = syn.CopulaDataGenerator()`                           | `g = syn.fPCADataGenerator()`                     |
|                                               | `g.fit(ds, syn.GaussianCopula())`                         | `g.fit(ds)`                                       |
|                                               | `g.generate(n_samples=500)`                               | `g.generate(n_samples=500)`                       |
|                                               |                                                           |                                                   |
| ![Source](../assets/img/temperature_true.png) | ![Gaussian](../assets/img/temperature_synth_gaussian.png) | ![fPCA](../assets/img/temperature_synth_fPCA.png) |

Table: Example application of Gaussian and fPCA classes in Synthia. Random profiles generated from a reduced source dataset of atmospheric temperature profiles (a) from the EUMETSAT Satellite Application Facility (SAF) on Numerical Weather Prediction (NWP) dataset (Eresmaa and McNally, 2014). The Gaussian copula (b) and fPCA (c) model is fitted to the data to generate statistically similar profiles. Data post-processing or plotting (not shown) can be separately as done for the source dataset as xarray dataset structure is kept by Synthia.


# Acknowledgments

We thank Maik Riechert for his comments and contributions to the project.


# References
