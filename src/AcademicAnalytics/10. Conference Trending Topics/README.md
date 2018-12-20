# Conference Trending Topics

This sample code illustrates how to find trending topics for a partitular conference series using USQL script and visualize the results using Power BI.

![](/images/PBIConferenceTrendingTopics(WWW).png "WWW trending topics") 


## Getting started

### ConferenceFieldsOfStudyByCitationGrowthRate.usql

Every paper in MAG has associated fields of study. We can find trending topics for a conference series by aggregating its papers. This script illustrates how calcuate Normalized Citation Growth Rate for fields of study that appeared in a given conference series.


#### Input Parameters

The script has the following parameters

| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  @conferenceShortName    | string | The conference series to perform analytics. The same analytics can be done for different conference series by changing this variable. `ConferenceSeries.NormalizedName` in Microsoft Academic Graph contains all possible values.|
|  @confFieldCitationGrowthRateStartYear    | int | The starting year for evaluating treading topics.|


#### Output Files

The script should output two tsv with headers. Here's what to expect

`conferenceFieldsOfStudy.tsv`

| FieldOfStudyId  | FieldName  | Level  | FieldMinYear | FieldMaxYear | NormalizedCitationGrowthRate | CitationCountIn5Year |
|-----------------|------------|--------|--------------|--------------|------------------------------|----------------------|
|     116537	  | Service provider | 2 | 1996 | 2018 | 22.336956521739129 | 137 |
|     2129575	  | Semantic Web	 | 2 | 1995	| 2018 | 108.27272727272727	| 397 |
|     ....        |   ....     | ....   |   ....       |   ....       |          ....                |      ....            |


`conferenceFieldsOfStudyYearlyStats.tsv`

| FieldOfStudyId  | Year | PublicationCount | CitationCount | AccumulativePublicationCount | AccumulativeCitationCount |
|-----------------|------|------------------|---------------|------------------------------|---------------------------|
|    115625	      |2013	 |       1	        |      85	    |              1	           |            85             |
|    459310	      |2001	 |       1	        |      51	    |              1	           |            51             |
|    ....         | .... |          ....    |  ....         |          ....                |         ....              |




### ConferenceTrendingTopics.pbit

The template visualizes the results using two line charts to compare trending topics' publication/citation count over time.
The template also has an additional slicer to filter trending topics by their field level for better comparison. 
 

#### Template Parameters
| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  ADL URI    | string | The URI of the Azure Data Lake Store where the script wrote its output. You can find this information through Azure Portal by navigating to [{Your data lake store instance}] -> [Overview] -> [Essentials]  |
| Conference Short Name | string | Used for finding the correct path to files output by the script. This should be the same value as @conferenceShortName in the script for the template to load correctly. |


### ConferenceTrendingTopics (WWW).pbix

This Power BI report file is for comparison. If you run the script as is then use ConferenceTrendingTopics.pbit to create a Power BI report, the visualization and interaction should be indentical. 

## Resources

- [Analytics & Visualization Samples for Academic Graph](https://github.com/Azure-Samples/academic-knowledge-analytics-visualization)
- [Microsoft Academic Website](https://academic.microsoft.com/)