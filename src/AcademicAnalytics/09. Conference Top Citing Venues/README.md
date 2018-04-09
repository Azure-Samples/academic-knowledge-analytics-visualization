# Conference Top Citing Venues

This sample code illustrates how to find top citing venues for a partitular conference series using USQL script and visualize the results using Power BI.

![](/images/PBIConferenceIncomingCitations(WWW).png "WWW incoming citations") 
![](/images/PBIConferenceIncomingCitationsByYear(WWW).png "WWW incoming citations by year") 


## Getting started

### AggregateConferenceReferencesByYearAndVenue.usql

This script illustrates how find incoming citations and aggregate them by venue and year.


#### Input Parameters

The script has the following parameters

| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  @conferenceShortName    | string | The conference series to perform analytics. The same analytics can be done for different conference series by changing this variable. `ConferenceSeries.NormalizedName` in Microsoft Academic Graph contains all possible values.|



#### Output Files

The script should output three tsv with headers. Here's what to expect

`conferenceYearlyIncomingCitationsByVenue.tsv`

| Year  | CitationVenueId  | CitationCount  |
|-------|------------------|----------------|
| 1994  |     18902827     |      2         |
| 1995  |     3084184      |      9         |
| ....  |     ....         |     ....       |


`conferenceIncomingCitationsByVenue.tsv`

| VenueId    |  CitationVenueId | CitationCount  |
|------------|------------------|----------------|
| 1135342153 |     255146       |      49        |
| 1135342153 |     414566       |      60        |
| ....       |     ....         |     ....       |


`venue.tsv`

| VenueId  |       VenueShortName      |      VenueName          |
|----------|---------------------------|-------------------------|
| 61661    | journal of prosthodontics |Journal of Prosthodontics|
| 2622674682  |     AICT      |      International Conference on Application of Information and Communication Technologies        |
| ....  |     ....      |     ....       |



### ConferenceOutgoingReferences.pbit

The template visualizes the results using a heatmap matrix and a Sankey diagram to illustrate the top referenced venues.

 

#### Template Parameters
| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  ADL URI    | string | The URI of the Azure Data Lake Store where the script wrote its output. You can find this information through Azure Portal by navigating to [{Your data lake store instance}] -> [Overview] -> [Essentials]  |
| Conference Short Name | string | Used for finding the correct path to files output by the script. This should be the same value as @conferenceShortName in the script for the template to load correctly. |

We duplicate `venue.tsv` in Power BI as TargetVenues/SourceVenues and use VenueId to connect them with ConferenceIncomingCitationVenues and ConferenceYearlyIncomingCitationVenues. This is similar to   [Conference Top Referenced Venues](/src/AcademicAnalytics/09.%20Conference%20Top%20Referenced%20Venues)

### ConferenceOutgoingReferences (WWW).pbix

This Power BI report file is for comparison. If you run the script as is then use ConferenceOutgoingReferences.pbit to create a Power BI report, the visualization and interaction should be indentical. 

## Resources

- [Analytics & Visualization Samples for Academic Graph](/README.md)
- [Visual Awesomeness Unlocked – Sankey diagram](https://powerbi.microsoft.com/en-us/blog/visual-awesomeness-unlocked-sankey-diagram/)
- [Use the Matrix visual in Power BI Desktop](https://docs.microsoft.com/en-us/power-bi/desktop-matrix-visual)
- [Microsoft Academic Website](https://academic.microsoft.com/)