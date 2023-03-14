# Methods

## Study Site
The focal UK wetland, the Somerset Levels and Moors (SLM) is one of the largest wetlands in the UK, covering 650km2 in the southwest of England, Somerset, with high biodiversity an active agricultural industry and tourism [@acremanTradeoffEcosystemServices2011]. Pumping of water and irrigation of these floodwaters, which began as early as the 9th century and intensified in the 20th century, means that much of this landscape has now been transformed into peat-based pastures primarily used for grazing. Since 1987, SLM has been subject to agri-environmental schemes that aim to enhance and integrate flood management and biodiversity ecosystem services in wetlands. The SLM provides key ecosystem services to local people and is a site of high biodiversity with notable numbers of wading and migratory birds resident throughout the year [@acremanTradeoffEcosystemServices2011]. 

To restore this environment to a more natural state while maintaining agricultural viability the SLM was denoted as an environmentally sensitive area [@morrisEconomicDimensionsIntegrating2008]. This agri-environmental scheme encouraging lower grazing pressure, reduced management of the fields and surrounding ditches during winter and spring periods, and most importantly stipulated a minimum water level in these areas which larger volumes of water being present all year round in these Tier 3 managed areas for enhanced flood management.


## Field Data Collection
We identified 17 locations in the SLM that had potential to harbour mosquito larvae and were equally split between Tier 3 (n = 9) and Tier 1 (n = 8) management schemes (Fig. 1). At each of these locations four plots connected by waterways were identified within a 500m and selected for sampling. Each site was sampled once in each of three seasons, spring (May), summer (June/July) and autumn (August/September), from 2009 to 2011. Invertebrates were collected from the sample sites using dip-netting: each sample site was comprised of 5-6 dip-points along the waterbody roughly one meter apart from each other. In each seasonal sampling period, each of these dip points was sampled 3 times, with care to dip both the centre and edges of the waterbody.   

We recorded the abundance of any macroinvertebrate species that were either mosquito larvae, or suspected/known predators of mosquito larvae, and aggregated these across all dips for each sampling site. We identified mosquitoes visually down to species or species complex level using the identification keys of @schaffnerMosquitoesEuropeIdentification2001. Other aquatic macroinvertebrate species were identified visually down to order and suborder where possible using @dobsonGuideFreshwaterInvertebrates2012. We estimated percentage cover and height of plant species in the area identified and once recorded to genus or species level we grouped them into functional structural types of vertical, emergent and floating vegetation (SUPP X). We also measured structural and physiochemical parameters of the waterbody at each sampling site averaged across all samples taken for each site (Table 2). 

## Statistical Analysis 
We used the R package Hierarchical Modelling of Species Communities (HMSC) framework to explore how biotic and abiotic interactions drive mosquito larval distribution across the SLM [@ovaskainenHowMakeMore2017; @ovaskainenJointSpeciesDistribution2020]. This implementation of a Bayesian multivariate hierarchical generalised mixed linear model aims to alleviate the interdependency of species responses to the environment and species responses to each other in the ecosystem, by modelling all species simultaneously and accounting for each species responses to measured and unmeasured environmental covariates through latent variable factors [@wilkinsonComparisonJointSpecies2019].  

We collected a total of 402 data points from 17 different sampling areas. To account for seasonality, we attempted sampling three times per year over a three-year period from 2009 to 2011. After excluding inaccessible areas and water bodies that were dried or drained during certain seasons and therefore unsuitable for sampling, we identified 320 unique sampling points that were used in our model and represent 67 distinct combinations of site, season, and year. In these unique sampling points, we excluded all species that occurred less than ten times to increase model stability [@ovaskainenJointSpeciesDistribution2020]. In this case we consider the presence of plant species as an abiotic driver as we expect them to function as a regulator of population fitness through shielding of predation or similar processes [@sahaHabitatComplexityReduces2009].  

To understand how biotic and abiotic factors determine mosquito population presence we utilised a multivariate probit model that was fitted to the presence-absence data obtained from our sampling sites with our abiotic covariates used as predictive variables on a linear scale (TableX). To account for potential spatial biases in the sampling data, we incorporated a distance matrix that represented the spatial scales between each sampling unit as a spatially structured random effect. Furthermore, we considered the impact of repeated sampling at sites and the temporal effects of sampling methods by including a nested random effect that accounted for both the year of sampling and the season within that year. In addition, we aimed to construct abundance models that included the same covariates, as we hypothesised that biotic interactions would have a greater impact on species abundance rather than species presence. However, due to the high complexity of the model, it was deemed computationally infeasible to achieve an acceptable fit [@howardImprovingSpeciesDistribution2014]. 

For model fitting we used the custom Bayesian sampling procedure from the HMSC package [@tikhonovHmscHierarchicalModel2022]. Each model was fitted with 4 MCMC chains with 1000 samples per chain at a thinning rate of 1000 for a total of 4 million MCMC samples in total. Convergence was measured using Gelman and Rubens potential scale reduction factor (PSRF), and values under >1.1 are considered converged [@gelmanInferenceIterativeSimulation1992]. Goodness of fit was measured using species-specific Tjur’s R2 values and the area under curve (AUC) statistic [@loboAUCMisleadingMeasure2008; @tjurCoefficientsDeterminationLogistic2009]. Predictive power of models was measured using k-fold (k=5) cross validation and measuring the AUC statistic. To better understand the drivers behind community composition we want to understand the importance of each predictor variable in our model. Here we can address the variance contributed to the model through each explanatory variable by performing variance partitioning analysis [see 69-70, @ovaskainenJointSpeciesDistribution2020]. 

To understand if management practices impact the presence of mosquitoes, we undertook a post-hoc analysis of all covariates that were significantly associated with mosquito presence. Bayesian multivariate models were built in the probabilistic programming language Stan using the BRMS package in R [@burknerBrmsBayesianRegression2022; @carpenterStanProbabilisticProgramming2017]. We modelled the significant covariates in separate models against management level as a categorical factor, with both a random effect for site and a nested random effect of season within year to account for spatiotemporal differences in covariate distribution.