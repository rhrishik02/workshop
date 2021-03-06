Word Count: ~1700


**Overview**


With poverty rampant on both global and local scales, reliable measurement and analysis becomes increasingly important. Unfortunately, traditional approaches to measuring poverty rely on outdated census data and data analysis techniques that are especially unreliable in low/middle income countries as they tend to lack necessary statistical infrastructure to conduct analyses. In recent years, scientists and researchers have turned to innovative approaches to measuring poverty and use newer-aged data science techniques to analyze indicators. The nature of identifiers and various measurements are still discussed among development experts within the research literature, ranging from construction of unidimensional and multidimensional indices to the use of monetary/nonmonetary metrics. 
Living standard indices are methods used to set appropriate thresholds under which a person is defined as poor, (i.e. poverty lines). Monetary based metrics identify poverty as a shortfall in consumption and measure whether households or individuals fall above or below a defined poverty line, whereas asset-based indicators define household welfare based on asset ownership, dwelling characteristics, and access to basic services like clean water and electricity. 
An analysis of poverty maps and their usefulness can be described as an evaluative inquiry. Specifically, with a central research question regarding what specific alleviations can be achieved using poverty maps, measuring the effectiveness of poverty maps becomes inherently evaluative. In other words, how effective are poverty maps for alleviation purposes?  Different approaches to map compilation depend on the type of methods and models data scientists use, thus altering the usefulness of the maps depending on what context they were compiled in. For example, some researchers will use data sets with similar features (e.g. night-time lights, building density, population measures) to create different maps ranging from population distributions to income disparity and consumption levels. Essentially, the usefulness of the maps boils down to three sub-research focuses of how accurate input data is, the methods and models used to compile the maps, and the surrounding context of possible alleviation resulting from maps.

**Data**


In “Mapping Poverty Using Mobile Phone and Satellite Data,” the authors use remote sensing and geographic information system data (RS) and call detail records data (CDR) for their models as RS and CDR data can capture complementary correlates of human behavior and living standards. Specifically, RS data of properties like temperature, rainfall and vegetation can provide insight about agricultural productivity while other physical properties like distance to roads, cities, and building density can provide insight about market productivity. Similarly, CDR data can provide information about monthly credit consumption and the proportion of people using mobile phones that indicate household access to financial resources, while movements of phones and the structure and geographical reach of the calling networks of individuals can correlate with remittance flows and economic opportunities. As RS and CDR data are generated at different spatial scales, they can be complementary by nature. 
To ensure accurate projections and resolutions, the raw CDR and RS data was processed by approximating mobile tower coverage using Voronoi tessellation, thus allowing the models to be built on the scale of Voronoi polygons. Each polygon was assigned RS and CDR values representing the mean, sum or mode of the corresponding data. The data was summarized and subsequently matched to the polygons based on the GPS located coordinates of PPI data, the latitude and longitude representing the centroid of each cluster, and the home tower of each income survey respondent.

![image](https://user-images.githubusercontent.com/78430530/116168176-d6f8c200-a6cf-11eb-9ecb-9a4876ff711f.png)


Figure 1. Spatial structure of Voronoi polygons based on the configuration of mobile phone towers in Bangladesh. The zoom window shows the spatial detail of Dhaka. (Taken from section 2.1) 



In “Estimation Of Poverty In Somalia Using Innovative Methodologies,” the researchers explain how the Somali High Frequency Survey (SHFS) was conducted and how it was used to estimate poverty in an otherwise data-deprived country. They first explain the rationale behind the sampling strategy used in the SHFS, then the data collection process, then the calculation of aggregate consumption, and finally the imputation of poverty in inaccessible areas. Data was collected using computer assisted personal interviews as this allowed for near-real time monitoring and quality control as a result of the large amount of instability in many regions. Consumption data was cleaned and then estimated based on food consumption, nonfood consumption, and consumption of durable assets. 


![image](https://user-images.githubusercontent.com/78430530/116168250-fbed3500-a6cf-11eb-8965-34f4b1531f6f.png)


Subsequently, spatial variables for poverty prediction were decided according to three main sources including a custom derived global database of over 300 spatial covariates from the WorldPop research group at the University of Southampton, geo‐tagged data from publicly  available sources, and population and population type data drawn from a novel population density map using recent data from OpenSteetMap, BMGF / Digital Globe spatial data, UNFPA survey and SHFS data. 15 variables with the highest correlation to poverty measures were then selected and used in the final model. 

**Method/Model**

To identify the set of predictors most suitable for modeling the 3 measures of WI, PPI, and income data, a model selection stage was first employed. For this, non-spatial generalized linear models were used to build every possible non-redundant model for every combination of covariates. The resulting models were then used in the hierarchical Bayesian geostatistical approach. Hierarchical Bayesian geostatistical models (BGMs) were employed to predict the three poverty metrics across the population. BGMs are used to estimate the parameters of a  posterior distribution where submodels form a hierarchical model and Bayes’ theorem is used to account for any uncertainty that is present. BGMs offer several advantages for addressing the limitations and constraints associated with modeling data including straightforwardly imputing missing data, allowing for the specification of prior distributions in model parameters and spatial covariance, and estimating uncertainty in the predictions as a distribution around each estimate. BGMs can also account for spatial autocorrelation through incorporating a spatially varying random effect. Finally, the geostatistical models defined for the WI, PPI and income data were applied to produce predictions of each poverty metric for Voronoi polygons as a posterior distribution with complete modelled uncertainty around estimates.

![image](https://user-images.githubusercontent.com/78430530/116168266-04de0680-a6d0-11eb-8267-f7f1d8a56da3.png)

Figure 2. National level prediction maps for mean WI (a) with uncertainty (d); mean probability of households being below $2.50/day (b) with uncertainty (e); and mean USD income (c) with uncertainty (f). Maps were generated using call detail record features, remote sensing data and Bayesian geostatistical models. The maps show the posterior mean and standard deviation from CDR–RS models for the WI and income data (a,c), and the RS model for the PPI (b). Red indicates poorer areas in prediction maps, and higher error in uncertainty maps. (Taken from section 2.5) 

Two main steps were used for model selection in the SHFS. First, a five-fold cross verification scheme was used to compare a range of model types. 4 folds of the data were randomly selected to be the training set and 1 fold of the data was randomly selected to be the testing set. Whichever model had the highest prediction in the testing set determined which models were selected, with R-squared and root square of mean error as goodness of fit measures - linear models produced the best results. Second, selection of covariates from the 15 aforementioned variables were refined using stepwise regression to maximize the predictive power of the linear models. The final model contained 12 covariates where each one was statistically significant in explaining the variation in poverty. Finally, to prevent the model from overfitting, 10% of the sample was randomly excluded and the process was repeated 1,000 times.


![image](https://user-images.githubusercontent.com/78430530/116168285-0d364180-a6d0-11eb-9c86-628e58e80dd8.png)

![image](https://user-images.githubusercontent.com/78430530/116168308-16271300-a6d0-11eb-8254-edc4e393b9b5.png)
![image](https://user-images.githubusercontent.com/78430530/116168317-1aebc700-a6d0-11eb-9241-6925cda3f417.png)



The authors attribute the large disparity in model accuracy (see R^2 in urban prediction vs. rural prediction) to poverty levels being largely spatially homogeneous in rural areas. In urban areas, the explanatory variables chosen do not vary significantly at a high enough spatial frequency relative to urban poverty estimates. In other words, poverty levels vary vastly in urban areas where areas with relatively lower levels of poverty are in close proximity to areas with relatively higher poverty levels. The authors note that other explanatory variables like building density and building patterns might improve the model. This emphasizes the importance of the previously mentioned sub-research focus of input data accuracy as having access to accurate input data would substantially increase the predictive power of the model. 

**Findings**


The researchers from the first article found that models employing both RS and CDR data outperformed models based on either of the sources alone, but also noted that some models that only employed CDR or RS separately performed nearly as well, subsequently attributing this independent success as context-dependent (e.g. models based on only RS data were more accurate in rural areas or models based on only CDR data were more accurate in cell-tower heavy areas) . This provides insight into the earlier identified sub-research focus of contextualizing poverty for alleviation as it becomes clear that in data-deprived regions, either RS or CDR input data might provide more accurate maps depending on the features of the area. In addition, they found that night-time lights, transport time to the closest urban settlement, climate, and elevation variables were important nationally and in rural models whereas distances to roads and waterways were significant in both urban and rural strata. Per cent nocturnal calls, and count and duration of SMS traffic were significant nationally. Mobility and social network features were important in all three strata. In urban areas, SMS traffic was important, whereas multimedia messaging and video attributes were key in rural areas.

![image](https://user-images.githubusercontent.com/78430530/116168341-26d78900-a6d0-11eb-9759-63aead3f5c37.png)
Figure 3. Out-of-sample observed versus predicted values for (a) DHS WI using mobile phone and remote sensing data: r2 = 0.76, n = 117, p < 0.001, RMSE = 0.394; (b) progress out of Poverty Index using remote sensing data: r2 = 0.32, n = 100, p < 0.001, RMSE = 57.439; and (c) income using mobile phone and remote sensing data: r2 = 0.27, n = 1384, p < 0.001, RMSE = 105.465. (Taken from section 3) 

The SHFS uses all the aforementioned techniques to create data and compile poverty maps from seemingly inaccessible areas. They arrived at relatively accurate estimations of poverty and were able to successfully compile the maps. From the SHFS, it was determined that 77% of the Somali population lived below the poverty line which was 26% higher than the unweighted average of low-income countries in sub-Saharan Africa, With the third highest poverty in the region, the GDP per capita was about $450 USD. 


![image](https://user-images.githubusercontent.com/78430530/116168440-5f776280-a6d0-11eb-8d62-97c2c236c1d6.png)

![image](https://user-images.githubusercontent.com/78430530/116168450-6605da00-a6d0-11eb-97bb-694714e9800e.png)



**Gaps**


It becomes evident from the two different methods that each has its advantages and disadvantages. The limitations of the model based on data from the SHFS arise from its inability to focus on specific spatial areas with a high enough resolution to be effective in urban areas  while the BGMs are limited by the lack of CDR data in areas that are too far from cell towers or not accounted for by RS. However, both models are feature based and this can prove to be extremely valuable for mapping poverty in otherwise inaccessible regions by taking advantage of these innovative input data streams. Overall, by viewing the effectiveness of the methods through the lens of the three sub-research focuses of accurate data, model use, and effective alleviation using a specific context, it becomes easier to understand the drawbacks of the models. I hope to encounter comprehensive alleviation strategies outside of just poverty identification in future papers. If methods are more inclusive of these 3 focuses, then effective poverty alleviation can be achieved.

Works Cited
Steele Jessica E., Sundsøy Pål Roe, Pezzulo Carla, Alegana Victor A., Bird Tomas J., Blumenstock Joshua, Bjelland Johannes, Engø-Monsen Kenth, de Montjoye Yves-Alexandre, Iqbal Asif M., Hadiuzzaman Khandakar N., Lu Xin, Wetter Erik, Tatem Andrew J. and Bengtsson Linus 2017 “Mapping poverty using mobile phone and satellite data” J. R. Soc. Interface.142016069020160690

Pape, Utz, and Luca Parisotto. "Estimating Poverty In A Fragile Context: The High Frequency Survey In South Sudan". 2019. World Bank, Washington, DC, doi:10.1596/1813-9450-8722. Accessed 10 Mar 2021.

Rue, Håvard et al. "Approximate Bayesian Inference For Latent Gaussian Models By Using Integrated Nested Laplace Approximations". Journal Of The Royal Statistical Society: Series B (Statistical Methodology), vol 71, no. 2, 2009, pp. 319-392. Wiley, doi:10.1111/j.1467-9868.2008.00700.x. Accessed 26 Apr 2021.

Gelfand, Alan E., and Sudipto Banerjee. "Bayesian Modeling And Analysis Of Geostatistical Data". Annual Review Of Statistics And Its Application, vol 4, no. 1, 2017, pp. 245-266. Annual Reviews, doi:10.1146/annurev-statistics-060116-054155.



	

