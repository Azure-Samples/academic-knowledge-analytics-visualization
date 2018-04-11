# Field of Study Top Authors


This sample code illustrates how to find top authors in a particular field of study by citation count using USQL and make the result interactive with Power BI.


![](/images/PBIFieldOfStudyTopAuthors(WWW).png "Computer science top authors")


## Getting started

### AggregateAuthorStatsInField.usql

This script illustrates how to aggregate stats for authors in a given field of study. 

#### Input Parameters

The script has the following parameters

| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  @fieldName    | string | The field of study name to perform analytics. The same analytics can be done for a different field of study by changing this variable. `FieldOfStudy.NormalizedName` in Microsoft Academic Graph contains all possible values.|
| @fieldTopAuthorsCount | int | Controls the number of rows to output to topAuthors.tsv. |


#### Output Files

The script should output one tsv with headers. Here's what to expect

`topAuthors.tsv`

| AuthorId | AuthorName  | CitationCount | PublicationCount |
|----------|-------------|---------------|------------------|
|2125104194|Philips S. Yu|    50136      |     1048         |
|2121939561|Jiawei Han   |    72259      |     702          |
|....      |....         |....           |....              |

### FieldTopAuthors.pbit

The template visualizes the results using a table with data bars and sort functionality. It also includes a slicer for users to search for particular authors in the table.

#### Template Parameters
| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  ADL URI    | string | The URI of the Azure Data Lake Store where the script wrote its output. You can find this information through Azure Portal by navigating to [{Your data lake store instance}] -> [Overview] -> [Essentials]  |
| Field Name | string | Used for finding the correct path to files output by the script. This should be the same value as @fieldName in the script for the template to load correctly. |


You can change top authors table sorting but understand that the topAuthors.tsv is constructed by taking top @fieldTopAuthorsCount authors by citation count. The table sort only compares the data in topAuthors.tsv.

There's also a slicer for author name. If you output lots of authors, you can find a specific author by using the slicer. The slicer is defaulted to single select, but the settings can be changed.

### FieldTopAuthors (Computer Science).pbix

This Power BI report file is for comparison. If you run the script as is then use FieldTopAuthors.pbit to create a Power BI report, the visualization and interaction should be indentical. 

## Resources

- [Analytics & Visualization Samples for Academic Graph](https://github.com/Azure-Samples/academic-knowledge-analytics-visualization)
- [Slicers in Power BI](https://docs.microsoft.com/en-us/power-bi/power-bi-visualization-slicers)
- [Working with tables in Power BI reports](https://docs.microsoft.com/en-us/power-bi/power-bi-visualization-tables)
- [Microsoft Academic Website](https://academic.microsoft.com/) 