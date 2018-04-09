# Conference Top Referenced Venues

This sample code illustrates how to find top referenced venues for a partitular conference series using USQL script and visualize the results using Power BI.

![](/images/PBIConferenceOutgoingReferences(WWW).png "WWW outgoing references") 
![](/images/PBIConferenceOutgoingReferencesByYear(WWW).png "WWW outgoing references by year") 


## Getting started

### AggregateConferenceReferencesByYearAndVenue.usql

This script illustrates how find outgoing references and aggregate them by venue and year.


#### Input Parameters

The script has the following parameters

| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  @conferenceShortName    | string | The conference series to perform analytics. The same analytics can be done for different conference series by changing this variable. `ConferenceSeries.NormalizedName` in Microsoft Academic Graph contains all possible values.|



#### Output Files

The script should output three tsv with headers. Here's what to expect

`conferenceYearlyReferenceVenue.tsv`

| Year  | ReferenceVenueId | ReferenceCount |
|-------|------------------|----------------|
| 1994  |     18902827     |      2         |
| 1995  |     3084184      |      9         |
| ....  |     ....         |     ....       |


`conferenceReferenceVenue.tsv`

| VenueId    | ReferenceVenueId | ReferenceCount |
|------------|------------------|----------------|
| 1135342153 |     414566       |      33        |
| 1135342153 |     985303       |      146       |
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

We duplicate `venue.tsv` in Power BI as TargetVenues/SourceVenues and use VenueId to connect them with ConferenceOutgoingReferenceVenues and ConferenceOutgoingYearlyReferenceVenues.

![](/images/PBIDuplicateRelationships.png "Create duplicate tables and manage their relationships") 

### ConferenceOutgoingReferences (WWW).pbix

This Power BI report file is for comparison. If you run the script as is then use ConferenceOutgoingReferences.pbit to create a Power BI report, the visualization and interaction should be indentical. 

## Resources

- [Analytics & Visualization Samples for Academic Graph](/README.md)
- [Visual Awesomeness Unlocked – Sankey diagram](https://powerbi.microsoft.com/en-us/blog/visual-awesomeness-unlocked-sankey-diagram/)
- [Use the Matrix visual in Power BI Desktop](https://docs.microsoft.com/en-us/power-bi/desktop-matrix-visual)
- [Microsoft Academic Website](https://academic.microsoft.com/)