# Conference Papers Basic Statistics

This sample code illustrates how to calculate basic paper statistics for a particular conference series using USQL and visualize the results with Power BI.


<iframe width="800" height="600" src="https://msit.powerbi.com/view?r=eyJrIjoiOTNhNGM5ZDItNDFjOC00NTk3LWE2NGEtNTI2NmExODNiOWY4IiwidCI6IjcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0NyIsImMiOjV9" frameborder="0" allowFullScreen="true"></iframe>


![](/images/PBIConferencePaperCount(WWW).png "WWW paper count")
![](/images/PBIConferenceReferenceCitationCount(WWW).png "WWW paper count")


## Getting started

### PaperYearlyStatisticsInConference.usql

This script illustrates how to aggregate publication count, average citation count and average reference count over year for a given conference series.


#### Input Parameters

The script has the following parameters

| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  @conferenceShortName    | string | The conference series to perform analytics. The same analytics can be done for different conference series by changing this variable. `ConferenceSeries.NormalizedName` in Microsoft Academic Graph contains all possible values.|



#### Output Files

The script should output one tsv with headers. Here's what to expect

`conferenceBasicStats.tsv`

| Year | PublicationCount  | AverageCitationCount | AverageReferenceCount |
|------|-------------------|----------------------|-----------------------|
| 1994 |        58         |         48.12069     |        5.862069       |
| 1996 |       104         |         50.66346     |        5.49038458     |
|....  |....               |....                  |....                   |

### ConferencePapersStatistics.pbit

The template visualizes the results using a column chart and a clustered column chart to illustrate the relationship between publication count, average citation count and average reference count over time. 

#### Template Parameters
| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  ADL URI    | string | The URI of the Azure Data Lake Store where the script wrote its output. You can find this information through Azure Portal by navigating to [{Your data lake store instance}] -> [Overview] -> [Essentials]  |
| Conference Short Name | string | Used for finding the correct path to files output by the script. This should be the same value as @conferenceShortName in the script for the template to load correctly. |


### ConferencePapersStatistics (WWW).pbix

This Power BI report file is for comparison. If you run the script as is then use ConferencePapersStatistics.pbit to create a Power BI report, the visualization and interaction should be indentical. 

## Resources

- [Analytics & Visualization Samples for Academic Graph](/README.md)
- [Scatter charts and bubble charts in Power BI ](https://docs.microsoft.com/en-us/power-bi/power-bi-visualization-scatter)
- [Microsoft Academic Website](https://academic.microsoft.com/) 


* [Conference Paper Statistics](/src/AcademicAnalytics/03.%20Conference%20Papers%20Basic%20Statistics/README.md)