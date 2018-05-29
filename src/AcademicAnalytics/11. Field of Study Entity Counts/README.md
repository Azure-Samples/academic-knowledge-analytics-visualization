# Field of Study Entity Counts

This sample code illustrates how to aggregate conference, journal, author and affiliation counts for each field of study using USQL script and visualize the results using Power BI.

![](/images/PBITopicEntityCountsOverTime.png "Topic entity counts over time") 

[Microsoft Academic](https://academic.microsoft.com/) also uses a similar calculation to power its Entity Type Analytics Page. Check out [Authors Analytics Page](https://academic.microsoft.com/#/authors/0/), [Conference Analytics Page](https://academic.microsoft.com/#/conferences/0/), [Journal Analytics Page](https://academic.microsoft.com/#/journals/0/), [Institution Analytics Page](https://academic.microsoft.com/#/institutions/0/) to see these stats in action. 

## Getting started


### AggregateFosEntityCount.usql

This script illustrates how find conference, journal, author and affiliation and aggregate them by field of study and year.


#### Input Parameters

The script has the no parameters. 


#### Output Files


The script should output two tsv with headers. Here's what to expect

`entityCountPerYearByFOS.tsv`

| FieldOfStudyId | Year  | EntityType  | Count  |
|----------------|-------|-------------|--------|
| 2777227988     | 2018  | Author      |  262   |
| 126255220      | 2018  | Conference  |  118   |
| ....           | ....  |   ....      |  ....  |


`fosDetails.tsv`

| FieldOfStudyId |          Name              |
|----------------|----------------------------|
|   12843        | gravitational singularity  |
|    4250        | sign function              |
| ....           | ....                       |



### TopicYearlyEntityCounts.pbit

The template visualizes the results using a line chart and a slicer to select the topic. 

 
#### Template Parameters
| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  ADL URI    | string | The URI of the Azure Data Lake Store where the script wrote its output. You can find this information through Azure Portal by navigating to [{Your data lake store instance}] -> [Overview] -> [Essentials]  |


### TopicYearlyEntityCounts.pbix

This Power BI report file is for comparison. If you run the script as is then use TopicYearlyEntityCounts.pbit to create a Power BI report, the visualization and interaction should be indentical. 

## Resources

- [Analytics & Visualization Samples for Academic Graph](https://github.com/Azure-Samples/academic-knowledge-analytics-visualization)
- [Microsoft Academic Website](https://academic.microsoft.com/)