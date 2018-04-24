---
layout: page
title: About
---

# Water

The PCA collects water data for ambient monitoring and point source regulation.  There a few sources of "water data" and all are substantial so it is good to refine your search.  

Ambient data are collected and stored by both the Watershed (Equis) and Watershed Pollutant Load Monitoring Network (Hydstra) programs.    

Wastewater data are collected by regulated parties and transferred to Tempo from the Regulated Services Portal (RSP).

## Wastewater

### **Monitoring data types**

Wastewater facilities are issued federal (**NPDES**) or state (**SDS**) permits.  Federal permits discharge to a surface water and state permits do not.  Both types of permits are required to submit monitoring data to the PCA.   

Facilities collect data and report data on daily, monthly, quarterly, and annual time periods.    

**Discharge Monitoring Reports (DMRs)** are the most common submittal and contain information influent and effluent results for each facility. The values can be monthly, quarterly, or yearly data.  Tempo contains data from 1998-present and pre-1998 information is available in a different format from the EPA PCS database.    

**Sample values** are the daily samples used to calculated DMR results.  These are submitted along with DMRs and stored in Tempo.  Digital sample values exist after 2014 and pre-2014 values are stored in scanned supplemental forms.    

**Annual reports** are required for various activities like land application of solids and sprayed waste.  These are stored in Tempo as scanned pdfs.


**Monitoring data categories**

Monitoring data are reported for surface discharge (**SD**), influent/internal waste (**WS**), groundwater monitoring (**GW**), ambient surface water (**SW**), and land application (**LA**) stations.    

Values are stored in Tempo **MONI** Subject Items and can have multiple attributes. Design flow and flow type are two commonly used.  Spatial data are collected and represented as GIS layers on the R-drive.    

Facility characteristics are stored on the treatment (**TREA**) subject item and contain attributes like NPDES status, EPA Major/Minor, Industrial/Municipal, and Facility Class.

### **Where to find data?**   
#### Facilities, permits, and requirements
The easiest place to start is in an existing Tableau report.

The first question may be "which facilities am I interested in?"  The [Facility Report](http://tableau/#/views/FacilityReport/Facandstndshbrd?:iid=4) provides facility details and spatial data.  This is a good starting point without being overwhelmed by monitoring data.   

Another logical question is "which permits are active."  The [permit list](http://tableau/#/views/Permitlist/Permitlist?:iid=4) shows effective wastewater permits by type and facility characteristic.

Reported values are a result of permit requirements.  The DMR reports display numeric limits, and the [limits and monitoring](http://tableau/#/views/wwpermitphaselimitsandmonitoring/Limitsandmonitoringwithphases) report shows the full permit requirements. 

**wh tempo:**If the information you seek is not contained in an existing Tableau report the schema deltaw.wh_tempo contains a number of useful data views.  The [Ranier page](https://rainier.pca.state.mn.us/documentation/DataDictionary/DELTAW/WH_TEMPO/tables.html) is a list of available data views with notes (for some).  

The most useful views are:

**ww facility:** A list of facilities with latest data from master file.

**mv trea details cf:** Facility treatment details from the central file.  This is useful for tracking change through time.

**mv si metadata mf:** The latest data about monitoring stations from the master file.

**mv dmr mon report:** The monthly monitoring data for 1999-present.

There are many other views with specific themes as well.



#### Monitoring results
There are two common reports for accessing monthly DMR data. Both contain the same information and and filters, one is a [dashboard](http://tableau/#/views/dmr_multiple_facility/FrontPage?:iid=2) and the other has filters on [each sheet](http://tableau/#/views/ww_standard_dmr_reports/DMRSummary_1).  Monthly DMR data are also available externally on the [Wastewater Data Browser](https://www.pca.state.mn.us/data/wastewater-data-browser).   

The internal applications are updated nightly and the external version is quarterly.  All values are shown "as reported" and may be revised as facilities amend DMRs.   

Daily sample values are available digitally after 2014 and found in the [Sample Values](http://tableau/#/views/dmr_sample_values/dailyDMRvalues) report.  Prior to the 2014 eDMR project the majority of sample values were stored as scanned pdfs or Excel files.    

#### Other submittals    
Annual reports are typically available as scanned documents.  Many of the annual reports are linked to the permit requirements for expected/received status but the data relationship is not perfect.  Use the [annual reports received list](http://tableau/#/views/AnnualReportsReceived/Annualreportsreceived?:iid=5) as a starting point.

### How to use wastewater data    
With data in hand there are a few things to consider.  No data source is perfect and with thousands of stations and millions of reported values you will find erroneous data.    

#### Permits and stations
It seems like "which stations are in my study area" would be a simple task.  Sadly, this is not always the case.  Historically location data were reported by PLS sections and as technology improved the permit application requested coordinates.  A coordinate improvement project in 2009 corrected 85% of the municipal SD stations.  Non-SD stations are still a work in progress, as are industrial SD stations.  Facility and station coordinates should **always** be reviewed.

#### Monitoring results    
Monitoring data are not automatically entered in the RSP from lab results.  The DMR form contains calculations for monthly average, total, and percent removal so operators calculate and enter data each month.  This introduces the possibility for calculation and transcription errors.  As data are reviewed facilities can revise (amend) DMRs with correct values.    

The most common and significant reporting error is the missing flow decimal point.  Facilities are required to report in million gallons per day (mgd) but smaller facilities often report a value of gallons.  Entering gallons and labeling it as million gallons quickly breaks an analysis.    

Other less common errors are concentration decimal points, switching monthly totals with averages, and not using all 30 days for monthly loading values.    
#### Loading calculations    
Pollutant loading calculations are a popular request in the among wastewater enthusiasts.  There is a lot of data manipulation to get a consistent and full multi-parameter dataset.  Effluent flow wasn't always reported on the SD station since the meter frequently measures flow entering the plant.  The DMRs reflect our changes in flow reporting strategy from SD to WS and back to SD.   

This requires a reference table pairing the correct flow station and type to the corresponding concentration.  There is also a patch table and rules to accommodate errant values.  Since not all facilities have full concentration datasets some loading values use annual average concentration or a categorical assumption from similar facilities.    

The resulting loads are assigned a confidence category indicating "Observed, Estimated from sample, or Estimated."  These categories are very important!

Now that you are caught up on loading data, [here they are!](http://tableau/#/views/Wastewaterpollutantloads/Introduction?:iid=1) 

## Groundwater


## Watersheds    
The [Watershed Pollutant Load Monitoring (WPLMN)](https://www.pca.state.mn.us/wplmn/overview) program collects ambient data for many streams and rivers.  It is a collaborative process and the group uses [FLUX32](https://www.pca.state.mn.us/wplmn/flux32) to calculate daily loads.    

Ambient watershed loads are available at the daily, annual, and average scales in a [Tableau application.](https://www.pca.state.mn.us/wplmn/data-viewer)    

Comparing ambient and point source pollutant loads is a tempting endeavor but should only be done with the necessary data stipulations.  Annual comparisons lose the impact on local stream conditions because wastewater's influence is greatest during summer months.  Stream flow is lower in late summer and oxygen levels decrease with increasing temperature so fish and aquatic insects are more easily stressed.
