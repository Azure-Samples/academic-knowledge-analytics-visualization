# Conference Top Authors By Static Rank

This sample code illustrates how to find top authors in a particular conference series by paper static rank using USQL and visualize the results with Power BI.

![](/images/PBIConferenceTopAuthorsByStaticRank(WWW).png "Computer science top authors")

## Getting started

### AuthorRankInConference.usql

This script illustrates how to aggregate static rank for authors and rank them in a given conference. 


#### Input Parameters

The script have the below parameters

| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  @conferenceShortName    | string | The conference series to perform analytics. The same analytics can be done for different conference series by changing this variable. `ConferenceSeries.NormalizedName` in Microsoft Academic Graph contains all possible values.|
| @conferenceTopAuthorsCount | int | Controls the number of rows to output to conferenceTopAuthorsByStaticRank.tsv. |


#### Output Files

The script should output one tsv with headers. Here's what to expect

`conferenceTopAuthorsByStaticRank.tsv`
| AuthorName | PublicationCount  | AuthorRank | AuthorNormalizedRank |
|----------|-------------|---------------|------------------|
|Wei-Ying Ma|   26   |    19      |     19         |
|Jure Leskovec|  39   |    11      |     20          |
|....      |....         |....           |....              |

### ConferenceTopAuthorsByStaticRank.pbit

The template visualizes the results using a scatter chart to compare the three dimensions publication count, rank, and normalized rank.

#### Template Parameters
| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  ADL URI    | string | The URI of the Azure Data Lake Store where the script wrote its output. You can find this information through Azure Portal by navigating to [{Your data lake store instance}] -> [Overview] -> [Essentials]  |
| Conference Short Name | string | Used for finding the correct path to files output by the script. This should be the same value as @conferenceShortName in the script for the template to load correctly. |

We made the top right corner of the scatter chart the "ideal" corner for easier visual consumption. Since we can't make Power BI show decreasing X/Y axes, we have to flip the rank from postive to negative. We did this by creating a measure with a formula of -1 * rank.
![](/images/PBISignFlipMeasure.png "flip sign using measure")


### ConferenceTopAuthorsByStaticRank (Computer Science).pbix

This Power BI report file is for comparison. If you run the script as is then use ConferenceTopAuthorsByStaticRank.pbit to create a Power BI report, the visualization and interaction should be indentical. 

## Resources

- [Analytics & Visualization Samples for Academic Graph](/README.md)
- [USQL RANK() Documentation](https://msdn.microsoft.com/en-us/azure/data-lake-analytics/u-sql/rank-u-sql)
- [Scatter charts and bubble charts in Power BI ](https://docs.microsoft.com/en-us/power-bi/power-bi-visualization-scatter)
- [Microsoft Academic Website](https://academic.microsoft.com/) 