---
title: 'swxg: A Python Package for Fast, Region-Agnostic Stochastic Weather Generation'
tags:
  - Python
  - swxg
  - stochastic
  - weather
  - generator
  - semiparametric
  - copula
authors:
  - name: Alexander B. Thames
    orcid: 0000-0003-4044-2471
    affiliation: 1
  - name: Antonia Hadjimichael
    orcid: 0000-0001-7330-6834
    affiliation: 1
  - name: Julianne D. Quinn
    orcid: 0000-0001-7806-4416
    affiliation: 2
affiliations:
  - name: Department of Geosciences, The Pennsylvania State University. University Park, Pennsylvania, USA.
    index: 1
  - name: School of Engineering and Applied Science, University of Virginia. Charlottesville, Virginia, USA.
    index: 2
date: 19 Aug 2025
bibliography: paper.bib
---

# Summary
The changing global climate affects all aspects of the global water cycle [@ipcc:2023]. In response, water resource managers must plan for how sectors like agriculture---which accounts for nearly 70% of global freshwater withdrawals and nearly 90% of global consumptive use [@iglesias:2015, @boretti:2019]---will evolve in a warmer future. Typical planning analyses of climate impacts follow a "top-down" methodology [@vano:2010, @cai:2015, @deb:2018, @zhao:2022] where hydroclimatic variables like precipitation and temperature are extracted from *a priori* scenarios from downscaled global circulation models, and then bias-corrected against local historical observations before being fed into hydrological or land-surface models whose outputs are analyzed for climate-induced impacts. But top-down methodologies and their underlying ensembles represent the lower bound on climate uncertainty [@stainforth:2007, @lamontagne:2018] due to issues separating the anthropogenic signal from natural variability [@najibi:2024], over- or underestimation of the hydroclimate from coarse grid sizes [@pierce:2015, @song:2020], and the effectively small set of analyzed "important" greenhouse gas concentration and/or socioeconomic scenarios [@pielke:2021].

Alternatively, "bottom-up" methodologies center the *deep uncertainties* [@lempert:2007, @kwakkel:2010, @brown:2020] associated with decision-making for climate change impacts. To do this they make use of exploratory modeling [@bankes:1993, @moallemi:2020] and stochastic sampling techniques to probe not just the conditions that are most likely but also other plausible but low-likelihood conditions, thereby supporting the *a posteriori* discovery of the most consequential scenarios [@bankes:2013, @nepomuceno-fernandez:2019]. In a water resources planning context, this process generally involves informing a stochastic model with hydroclimatic parameters from a host of regionally downscaled climate projections to then create a broader ensemble of counterfactual, modeled states of the world that are treated as inputs for the hydrologic or land-surface models used in impact analyses [@hadjimichael:2020a, @hadjimichael:2020b, @quinn:2020].

Stochastic weather generators (SWGs) are suitable exploratory modeling tools for exploratory climate impact analyses as they are statistical models that can simulate realistic, arbitrarily long sequences of regionally-informed meteorological variables like precipitation and temperature [@gabriel:1962, @richardson:1981, @wilks:1999, @ailliot:2015]. Critically, SWGs must be *multivariate* and *multisite* [@van-wart:2015, bureau-of-reclamation:2022] to account for both the region-specific spatiotemporal correlations and nonlinearities between hydroclimatic variables [@li:2019]. To this end we have developed `swxg`, a Python-based package that allows users to easily and quickly synthesize regionally-correlated weather variables based on an input set of observations through the state-of-the-art methodology of the semiparametric generation of precipitation followed by the conditional, copula-based generation of temperature. Included in the package are also methods to validate how the data has been fit, and how the synthetic weather compares to the observed weather.

# Design Architecture
Figure \autoref{swxgarch} outlines the typical `swxg` workflow along with example functions that are called in each step. Documentation of all functions can be found in the `swxg` [API]().

![](swxgarch.svg)\label{swxgarch}

# Statement of Need
Climate change is impacting human-natural systems like agriculture by altering regional hydroclimatic properties like mean temperature, precipitation, humidity, soil moisture, runoff, and plant evapotranspiration, as well as the frequency and magnitude of regional hazards like floods and droughts [@olmstead:2014, @crimmins:2023]. Because the deep uncertainties inextricable from climate change produce futures of unknown consequence for regional stakeholders, exploratory modeling of the hydroclimate is a valuable approach to comprehensively identify the most important drivers of change and vulnerabilities to different stakeholders [@gupta:2024]. The unique compounding influence of climate change on water availability in the western US---specifically the Upper Colorado River Basin in the state of Colorado---has prompted several regional bottom-up climate impact analyses for streamflow [@bracken:2014, @hadjimichael:2020b, @quinn:2020, @gold:2024] to support hydrological decisionmaking surrounding supply water to nearly 40 million people across seven states, 30 tribal nations, and Mexico, contributing nearly $1.4T USD to the regional and national economy [@james:2014].

`swxg` was originally designed to expand the existing regional exploratory analysis from just streamflow to include agricultural consumptive use as well through integration with the Colorado Decision Support System's consumptive use model StateCU [@statecu:2021]. However, given lack of contemporary weather generators for Python and the universality of the inputs to `swxg` of `location`, `time`, `precipitation`, and `temperature`, this package has evolved past its initial use case to support any stochastic weather generation for any reason. The API for `swxg` was created with simplicity and speed in mind, build around a class-based structure with which users interface with only two methods: `fit()` and `synthesize()`. Options for how to fit the observations, how to generate the synthetic data, and how to validate both the fits and the synthetics are included by default to concisely provide both functionality and corroboration. Fitting and synthesizing data are explicitly kept as two separate steps to support the (external) exploration of states of the world. The paper first using `swxg` is currently in preparation, and in this paper the fitting and synthesizing methodology is described in detail. Overall, `swxg` broadens the accessibility of state-of-the-art weather generation for exploratory modeling and beyond by massively streamlining the fitting, synthesizing, and validating process. 

# Acknowledgments
Acknowledgments to come!

# References
