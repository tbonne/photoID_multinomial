# Extracting spatial networks from capture-recapture data reveal structured habitat use within a marine mammal’s spatial range
<br>

### Abstract: 
1.	Estimating the impacts of anthropogenic disturbances requires an understanding of the habitat use patterns of individuals within a population. This is especially the case when disturbances are localized within a population’s spatial range, as variation in habitat-use within a population can drastically alter the distribution of impacts. 
2.	Here, we illustrate the potential for multilevel multinomial models to generate spatial networks from capture-recapture data, a common data source use in wildlife studies to monitor population dynamics and habitat use. These spatial networks capture which regions of a population’s spatial distribution share similar/dissimilar individual usage patterns, and can be especially useful for detecting structured habitat use within the population’s spatial range.
3.	Using simulations and 18 years of capture-recapture data from St. Lawrence Estuary (SLE) beluga, we show that this approach can successfully estimate the magnitude of similarities/dissimilarities in individual usage patterns across sectors, and identify sectors that share similar individual usage patterns that differ from other sectors, i.e., structured habitat use. In the case of SLE beluga, this method identified multiple clusters of individuals, each preferentially using restricted areas within their summer range of the SLE. 
4.	Synthesis and applications. Multilevel multinomial models can be effective at estimating spatial structure in habitat use within wildlife populations sampled by capture-recapture of individuals. Our finding of a structured habitat use within the SLE beluga summer range has direct implications for estimating individual exposures to localized stressors, such as underwater noise from shipping or other activities. 

 
<br>
 
### Code:

 In this paper we used brms to build and run a multilevel multinomial model to create population-level spatial networks. See [this link](https://github.com/tbonne/photoID_multinomial/blob/main/R/multinomial_code.Rmd) for more detailed code, but below is the general formula used:
 
  bf(y | trials(totsize) ~ 1 + (1|p|ID)) + multinomial()
  
 Here 'y' is a column vector with the number of times a beluga was seen in each sector of the St. Lawrence Estuary. 'Totsize' is the total number of times that beluga was seen, and 'ID' is the individual beluga ID number. The additional 'p' in the random effects formula (1|p|ID) allows correlations between individual random intercepts (i.e., beluga usage patterns) to be calculated between sectors.
<br>
 
### Visualizations:
 We can visualize these correlations between beluga usage patterns (i.e., similarities in individual random intercepts) between sectors:
 
 ![](inst/figs/Fig_relative_use_randomEffects.png)
 
 *Figure 1: Estimate of the relative use (i.e., deviation from mean use) for each individual within the SAG (a) and CTE sectors (b) of the St. Lawrence beluga summer habitat. The values are deviations from the mean probability of observing individuals within a sector and are on the logit scale. The red dashed line represents the mean use, black points represent the estimated deviation from the mean, while the horizontal grey lines represent the 95% credible interval. To highlight how correlations are estimated between sectors, the estimated top 10 users of the SAG sector are represented by blue dots (panel a), and those same individuals are also highlighted in blue in the CTE sector (panel b).*
 
 
 We also use these between sector correlations to create a population spatial network defining similarity/dissimilarity in beluga usage patterns within the St.Lawrence Estuary:
 
 ![](inst/figs/Spatial_comm_net.png)

*Figure 4: Similarity and dissimilarity between sectors in the beluga whale population of the St. Lawrence. The green edges between two sectors signify that the sectors share high/low users, while red edges signify that they have dissimilar high/low users. The lack of an edge signifies that the high/low users of one sector does not provide information about the high/low users of other sectors. Nodes represent sectors, and are coloured based on shared communities: i.e., shared green edges, and no red edges. Node sizes represent the magnitudes of individual differences in use within the sector, i.e., larger nodes suggest larger differences between high and low users.*
