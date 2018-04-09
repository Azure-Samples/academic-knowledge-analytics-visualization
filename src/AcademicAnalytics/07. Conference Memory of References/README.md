# Conference Memory of References

This sample code illustrates how to aggregate paper reference information for a partitular conference series using USQL script and visualize the results using Power BI.

![](/images/PBIConferenceMemoryOfReferences(WWW).png "WWW memory of references") 

## Getting started

### AggregateConferenceReferencesByYear.usql

This script illustrates how aggregate reference count by conference paper publication year and referenced paper publication year.


#### Input Parameters

The script has the following parameters

| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  @conferenceShortName    | string | The conference series to perform analytics. The same analytics can be done for different conference series by changing this variable. `ConferenceSeries.NormalizedName` in Microsoft Academic Graph contains all possible values.|



#### Output Files

The script should output one tsv with headers. Here's what to expect

`conferenceReferenceMemory.tsv`

| Year  | ReferenceYear | ReferenceCount |
|-------|---------------|----------------|
| 1998  |     1996      |      212       |
| 2000  |     1992      |      26        |
| ....  |     ....      |     ....       |


### ConferenceMemoryOfReferences.pbit

The template visualizes the results using a heatmap matrix to illustrate what year of publications are most referenced for each conference instance.

 

#### Template Parameters
| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  ADL URI    | string | The URI of the Azure Data Lake Store where the script wrote its output. You can find this information through Azure Portal by navigating to [{Your data lake store instance}] -> [Overview] -> [Essentials]  |
| Conference Short Name | string | Used for finding the correct path to files output by the script. This should be the same value as @conferenceShortName in the script for the template to load correctly. |


### ConferenceMemoryOfReferences (WWW).pbix

This Power BI report file is for comparison. If you run the script as is then use ConferenceMemoryOfReferences.pbit to create a Power BI report, the visualization and interaction should be indentical. 

## Resources

- [Analytics & Visualization Samples for Academic Graph](/README.md)
- [Use the Matrix visual in Power BI Desktop](https://docs.microsoft.com/en-us/power-bi/desktop-matrix-visual)
- [Microsoft Academic Website](https://academic.microsoft.com/)