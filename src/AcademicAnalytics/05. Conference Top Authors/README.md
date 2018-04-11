# Conference Top Authors

This sample code illustrates how to find top authors for a particular conference series using USQL and visualize the results with Power BI.

![](/images/PBIConferenceTopAuthorsScatterChart(WWW).png "WWW top authors scatter chart") 
![](/images/PBIConferenceTopAuthorsYearHeatmap(WWW).png "WWW top authors citation year heatmap")
![](/images/PBIConferenceTopAuthorsTable(WWW).png "WWW top authors table")


## Getting started

### ConferenceTopAuthors.usql

This script illustrates how to find top conference authors based on citation count and top cited authors for a given conference series.


#### Input Parameters

The script has the following parameters

| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  @conferenceShortName    | string | The conference series to perform analytics. The same analytics can be done for different conference series by changing this variable. `ConferenceSeries.NormalizedName` in Microsoft Academic Graph contains all possible values.|



#### Output Files

The script should output three tsv with headers. Here's what to expect

`conferenceTopAuthors.tsv`

| AuthorName  |      DetailsUrl        | PublicationCount | CitationCount | AuthorCitationRank | AuthorPublicationRank |
|-------------|------------------------|------------------|---------------|--------------------|-----------------------|
|Jure Leskovec|https://academic.microsoft.com/#/detail/1878631932| 39 | 3459 | 16 | 1 |
|Ravi Kumar   |https://academic.microsoft.com/#/detail/2130754085| 29 | 5970 | 4 | 2  |
|....         |....                                              |....|.... |....|....|


`conferenceMostCitedAuthors.tsv`

| AuthorName  | AuthorId |      DetailsUrl        | PublicationCount | CitationCount |
|-------------|----------|------------------------|------------------|---------------|
|Jure Leskovec|1878631932|https://academic.microsoft.com/#/detail/1878631932| 106 | 949 |
|Sergey Brin  |2052648321|https://academic.microsoft.com/#/detail/2052648321| 9 | 412 |
|....         |...       |....                                              |....|....|


`conferenceCitedAuthorsByYear.tsv`

| AuthorId | Year | CitationCount |
|----------|------|---------------|
| 57747768 | 1995 |       5       |
| 237419955| 1995 |       2       |
| ....     | .... |    ....       |

### ConferenceTopAuthors.pbit

The template has two report pages and visualizes the results using tables with data bars, a scatter chart and a matrix heatmap.

The matrix heatmap ilustrates how most cited author changes over time. 

 The use of the tables with data bars is similar to the [Field of Study Top Authors](/src/AcademicAnalytics/01.%20Field%20of%20Study%20Top%20Authors) sample. 
 
 The scatter chart is similar to [Conference Top Authors By Static Rank](/src/AcademicAnalytics/02.%20Conference%20Top%20Authors%20By%20Static%20Rank)

#### Template Parameters
| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  ADL URI    | string | The URI of the Azure Data Lake Store where the script wrote its output. You can find this information through Azure Portal by navigating to [{Your data lake store instance}] -> [Overview] -> [Essentials]  |
| Conference Short Name | string | Used for finding the correct path to files output by the script. This should be the same value as @conferenceShortName in the script for the template to load correctly. |


We used AuthorId to connect TopCitedAuthorsByConferencePapers and YearlyTopCitedAuthorsByConferencePapers.

![](/images/PBIConnectRelationships.png "Create table relationships")

This allows the matrix heatmap visual to display author name and enables filtering.

![](/images/PBIConferenceTopAuthorsFilter(WWW).png "Using a visual to filter other visuals")

### ConferenceTopAuthors (WWW).pbix

This Power BI report file is for comparison. If you run the script as is then use ConferenceTopAuthors.pbit to create a Power BI report, the visualization and interaction should be indentical. 

## Resources

- [Analytics & Visualization Samples for Academic Graph](https://github.com/Azure-Samples/academic-knowledge-analytics-visualization)
- [Use the Matrix visual in Power BI Desktop](https://docs.microsoft.com/en-us/power-bi/desktop-matrix-visual)
- [Create and manage relationships in Power BI Desktop](https://docs.microsoft.com/en-us/power-bi/desktop-create-and-manage-relationships)
- [Microsoft Academic Website](https://academic.microsoft.com/)