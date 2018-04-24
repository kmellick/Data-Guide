---
layout: page
title: GIS
---  

## Where to find MPCA (and other agencies') data?    
Currently the R:\ drive is an excellent collection of spatial data.  In the age of sharing and public data the new [Geospatial Commons](https://gisdata.mn.gov/)  rose to take R-drive's place.  The Geospatial Commons has a home on the L:\ drive so datasets can participate in both internal and external data gatherings.    

You may continue to find useful things in the R-drive but it will eventually be decommissioned.


## Land use maps {#landuse}
Land use shapefiles are maintained by MPCA GIS technical staff and stored on the agency R-drive at `R:\landuse_landcover`.


## United States Census boundaries {#census}

Copies if the USCB Census shapefiles are stored on the agency R-drive at `R:\Demographics .  This includes the decennial census boundaries but not the 5-year average ACS data.  

Census boundaries can be loaded into R using the `tigris` package to map air data to Census tracts and block groups. Use the following code to map MN boundaries.
```{r, eval = F}
# This script downloads shapefiles of Minnesota Census boundaries  
# Load packages
library(tigris)

# Load boundaries
county_bnds <- counties(state = "MN", cb = T)

tract_bnds  <- tracts(state = "MN", cb = T)

bg_bnds     <- block_groups(state = "MN", cb = T)

# Plot 
plot(county_bnds)
```


### American Community Survey (ACS) {#acs}
The ACS provides updated demographic statistics used for population estimates and Environmental Justice indicators.  


Minnesota ACS results can be loaded into R using the `tidycensus`. Use the following code to download updated population and income estimates.
```{r, eval = F}
# This script downloads American Community Survey (ACS) results for MN
# Load packages
library(tidycensus)

# ACS data requires a Census key
# Visit: http://api.census.gov/data/key_signup.html
census_api_key("Your_API_key")

# View all ACS variables
acs_variables <- load_variables(2015, "acs5", cache = TRUE)

# Download 5-yr population estimates for 2015
pops_2015 <- get_acs(geography = "tract", 
                     state     = "MN", 
                     variables = "B01003_001", 
                     survey    = "acs5", 
                     year      = 2015)

# Download decennial population estimates for 2010
pops_2010 <- get_decennial(geography = "tract", 
                           state     = "MN", 
                           variables = "P0080001", 
                           year      = 2010)

# Download household median income for 2015
med_inc_2015 <- get_acs(geography = "tract", 
                        state     = "MN", 
                        variables = "B19013_001", 
                        survey    = "acs5", 
                        year      = 2015)
```



