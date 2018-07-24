# Field of Study Top Entities

This sample code illustrates how to find top entities by Microsoft Academic Rank, H-Index, Estimated Citations and time range for all fields of study using USQL script and visualize the results using Power BI. 

![](/images/PBIFieldOfStudyTopEntities.png "Field of study top entities") 


[Microsoft Academic](https://academic.microsoft.com/) also uses similar calculation to power its Entity Type Analytics Page. Check out [Authors Analytics Page](https://academic.microsoft.com/#/authors/0/), [Conference Analytics Page] (https://academic.microsoft.com/#/conferences/0/), [Journal Analytics Page] (https://academic.microsoft.com/#/journals/0/), [Institution Analytics Page] (https://academic.microsoft.com/#/institutions/0/) to see these stats in action. 


## Getting started

### FieldTopEntities.usql

This script illustrates how find top enities for each field of study by calculating Microsoft Academic Rank, H-Index, and Estimated Citations. The calculation is also done for three different time ranges, all time, past 5 years, and past 10 years. 


#### Input Parameters

The script has the following parameters

| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
| @topEntitiesCount | int | Controls the number of rows to output to EntityStatsByFOS.tsv. |



#### Output Files

The script should output three tsv's with headers. Here's what to expect

`EntityStatsByFOS.tsv`

| FieldOfStudyId  | EntityId  | EntityType  |  TimeRange  |  Rank  |  EstimatedCitation  |  HIndex  |
|-----------------|-----------|-------------|-------------|--------|---------------------|----------|
| 88463610        | 2688312817| Author      |  5yr        |  21243 |      1              |   1      |
| 2780100698      | 71285955  | Journal     |  All        |  17051.240073  |  6603       |  41      |
| ....            | ....      | ......      |  .........  |  ....  |  .....              |  ....    |



`EntityDetails.tsv`

| EnityId    |      Name        |
|------------|------------------|
| 209317618  |  Kevin M Gowdie  |
| 1291425158 |     Google       |
| ....       |     ....         |


`FOSDetails.tsv`

| FieldOfStudyId  |       Name      |
|-----------------|-----------------|
| 4250            | sign function   |
| 678711          | labeling theory |
| ....            | ....            |



### TopicTopEntities.pbit

The template visualizes the results using a table and three slicers for filtering.
 

#### Template Parameters
| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  ADL URI    | string | The URI of the Azure Data Lake Store where the script wrote its output. You can find this information through Azure Portal by navigating to [{Your data lake store instance}] -> [Overview] -> [Essentials]  |


### TopicTopEntities.pbix

This Power BI report file is for comparison. If you run the script as is then use TopicTopEntities.pbit to create a Power BI report, the visualization and interaction should be indentical. 

## Resources

- [Analytics & Visualization Samples for Academic Graph](https://github.com/Azure-Samples/academic-knowledge-analytics-visualization)
- [Slicers in Power BI](https://docs.microsoft.com/en-us/power-bi/power-bi-visualization-slicers)
- [Microsoft Academic Website](https://academic.microsoft.com/)