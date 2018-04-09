# Conference Top Institutions

This sample code illustrates how to find top institutions for a particular conference series using USQL and visualize the results with Power BI.

![](/images/PBIConferenceTopInstitutionsTable(WWW).png "WWW top institutions table") 
![](/images/PBIConferenceTopInstitutionsScatterChart(WWW).png "WWW institutions scatter chart")


## Getting started

### ConferenceTopInstitutions.usql

This script illustrates how to find top institutions based on citation for a given conference series.


#### Input Parameters

The script has the following parameters

| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  @conferenceShortName    | string | The conference series to perform analytics. The same analytics can be done for different conference series by changing this variable. `ConferenceSeries.NormalizedName` in Microsoft Academic Graph contains all possible values.|



#### Output Files

The script should output one tsv with headers. Here's what to expect

`conferenceTopInstitutions.tsv`

| InstitutionName  |      DetailsUrl        | PublicationCount | CitationCount | InstitutionCitationRank | InstitutionPublicationRank |
|-------------|------------------------|------------------|---------------|--------------------|-----------------------|
|  Microsoft  |https://academic.microsoft.com/#/detail/1290206253| 419 | 21651 | 3 | 1 |
|Stanford University  |https://academic.microsoft.com/#/detail/97018004| 156 | 28644 | 1 | 5  |
|....         |....                                              |....|.... |....|....|


### ConferenceTopInstitutions.pbit

The template visualizes the results using a table with data bars and scatter chart.

 The use of the tables with data bars is similar to the [Field of Study Top Authors](/src/AcademicAnalytics/01.%20Field%20of%20Study%20Top%20Authors) sample. 
 
 The scatter chart is similar to [Conference Top Authors By Static Rank](/src/AcademicAnalytics/02.%20Conference%20Top%20Authors%20By%20Static%20Rank) sample.

#### Template Parameters
| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  ADL URI    | string | The URI of the Azure Data Lake Store where the script wrote its output. You can find this information through Azure Portal by navigating to [{Your data lake store instance}] -> [Overview] -> [Essentials]  |
| Conference Short Name | string | Used for finding the correct path to files output by the script. This should be the same value as @conferenceShortName in the script for the template to load correctly. |


### ConferenceTopInstitutions (WWW).pbix

This Power BI report file is for comparison. If you run the script as is then use ConferenceTopInstitutions.pbit to create a Power BI report, the visualization and interaction should be indentical. 

## Resources

- [Analytics & Visualization Samples for Academic Graph](/README.md)
- [USQL RANK() Documentation](https://msdn.microsoft.com/en-us/azure/data-lake-analytics/u-sql/rank-u-sql)
- [Scatter charts and bubble charts in Power BI ](https://docs.microsoft.com/en-us/power-bi/power-bi-visualization-scatter)
- [Microsoft Academic Website](https://academic.microsoft.com/)