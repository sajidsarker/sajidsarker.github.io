---
layout: post
title: Economic Program Interventions in Urban Poverty Alleviation
date: 2022-11-19 15:23:00
tags: [Machine Learning, Economics, Econometrics, Research, Data Science]
---
## Economic Program Interventions in Urban Poverty Alleviation

In 2016, I conducted Development Economics research at the *Bangladesh Institute for Development Studies* (BIDS). It is an institute subordinate to the *Ministry of Planning* (Bangladesh) involved in academic research in the field of economics to provide policy-prescriptions and governmental economic planning.

One of the myriad projects I undertook in collaboration with DSK-Shiree (NGO) included a panel data study of urban populations in the capital of Dhaka existing at or below the national poverty line.

As an observational study of select households surveyed in a *randomised control trial* (RCT) spanning two rounds for the years 2011 and 2015, the goal of the programme was to determine whether certain urban poverty alleviation economic interventions lead to anticipated positively associated outcomes for households.

The desired outcomes were for households to achieve socioeconomic growth and development across various indicators as a result of prescribed interventions applied across experimental groups, while withheld from a control group in 2011. The interventions associated with the best socioeconomic outcomes observed in 2015 were then applied to all households participating in the study as a matter of both ethical and humanitarian policy.

In this research, the unit of analysis was at the household level. The various models I produced included:
- Impact on healthcare-seeking behaviour
- Impact on log income
- Impact on housing conditions
- Impact on choice of water source
- Impact on household hygiene
- Impact on nutrition
- Impact on food consumption
- Impact on perception of economic mobility

The dataset represented an unbalanced panel dataset where it was possible to an extent to observe the changes in these indicators for a household across the (2) periods in order to glean the magnitude and direction of impact.

These impacts were modelled by multiple linear regression as well as multinomial logit while controlling for:
- Exogenous shocks
- Time variant and invariant factors
- Observed heterogeneities in household characteristics
- Stratified sampling of impoverished urban populations
- Household and ancestral wealth
- Geographical origin

Policy prescriptions which were tested on treatment versus the control sample of urban population included:
- Education
- Training
- Stipends
- Government stamps for free access

Multinomial logit models are particularly helpful in measuring the likelihoods that households pursue certain behaviours that are being incentivised such as improved hygiene, food consumption, seeking healthcare, and water source choices to their advantage subject to a programmatic policy prescription. Other indicators were observed to determine which policy prescriptions lead to the most positive impact on incomes, housing conditions, nutrition, and perception of economic mobility. This has all been structured under the implicit assumption that increased household incomes lead to increased consumption and therefore an improved standard of living, *ceteris paribus*.
