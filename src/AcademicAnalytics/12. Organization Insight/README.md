# Organization Insight

This sample code illustrates how to create a MAG subgraph for an organization(affiliation) using USQL script. Then, create an interactive report by visualizing the subgraph using Power BI.

`Organization Insight: Overview`
![](/images/OrgInsight_Overview_1.png "Organization Insight Overview Page 1")
![](/images/OrgInsight_Overview_2.png "Organization Insight Overview Page 2")

`Organization Insight: Topic Performance`
![](/images/OrgInsight_TopicPerformance_1.png "Organization Insight Topic Performance Page 1")
![](/images/OrgInsight_TopicPerformance_2.png "Organization Insight Topic Performance Page 2")

`Organization Insight: Author Performance`
![](/images/OrgInsight_AuthorPerformance_1.png "Organization Insight Author Performance Page 1")
![](/images/OrgInsight_AuthorPerformance_2.png "Organization Insight Author Performance Page 2")
![](/images/OrgInsight_AuthorPerformance_3.png "Organization Insight Author Performance Page 3")

`Organization Insight: Topic Relationships`
![](/images/OrgInsight_TopicRelationships.png "Organization Insight: Topic Relationships Page")

`Organization Insight: Partner Relationships`
![](/images/OrgInsight_PartnerRelationships.png "Organization Insight: Partner Relationships Page")



## Getting started


### GenerateSubgraphForAffiliation.usql

This script illustrates how create a subgraph that contains paper, author, partner affiliation, venue, field of study information for an affiliation. 


#### Input Parameters

The script has the following parameters

| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  @organizationName    | string | The organization to generate MAG subgraph for. The MAG subgraph can be generated for different organization by changing this variable. The `Affiliation.NormalizedName` table column in Microsoft Academic Graph contains all possible values for this parameter.|
|  @organizationPaperMinYear    | int | Controls what papers will be included in the subgraph based on publication year. To include all papers possible, use `0`|


#### Output Files


The script should output 10 tsv with headers. Here's what to expect

`Affiliation.tsv`

| AffiliationId   | AffiliationName|
|-----------------|----------------|
| 1290206253      | Microsoft      |

***This table should include only 1 row***


`Partner_Affiliation.tsv`

| AffiliationId   | AffiliationName                 |
|-----------------|---------------------------------|
| 74973139        | Carnegie Mellon University      |
| 102322142       | Rutgers University              |
| ....            | ....           |


`Paper.tsv`

| PaperId        |                   Title                                         |  CitationCount   |  Date  |  PublicationType |   LogProb   |                   Url                            |  VId    |  Year   |
|----------------|-----------------------------------------------------------------|------------------|--------|------------------|-------------|--------------------------------------------------|---------|---------|
|   1509054498   | Structure From Motion Sparse Versus Dense Correspondence Methods|         14       |1/1/1999| Conference       | 6.54598E-10 |https://academic.microsoft.com/#/detail/1509054498 |1163163559| 1999  |
|   1509084262   | System And Method For Changing The Characteristics Of A Button By Direct Manipulation |         122       |4/1/1997| Patent       | 3.7332E-09 |https://academic.microsoft.com/#/detail/1509084262 | | 1997  |
| ....           | ....                                                            |   ....           | ....   | ....             | ....        | ....                                              | ....     | ....  |


`Author.tsv`

|    AuthorId    |          AuthorName        |
|----------------|----------------------------|
|   2655371076   |    Ming-Chieh Lee          |
|   221619374    |    Denis Y. Altudov        |
| ....           | ....                       |


`Partner_Author.tsv`

|    AuthorId    |          AuthorName        |
|----------------|----------------------------|
|   4787260      |    Philip A. MacFaul       |
|   18851973     |    Nikos Mamoulis          |
| ....           | ....                       |


`PaperAuthorAffiliationRelationship.tsv`

| PaperId     |  AuthorId   |   AffiliationId   | AuthorSequenceNumber |
|-------------|-------------|-------------------|----------------------|
| 161551      | 2075955518  |   1290206253      |          1           |
| 11720368    | 2583637510  |   1290206253      |          3           |
| ....        | ....        | ....              | ....                 |

***All AffiliationId in this table is expected to have the same value***


`Partner_PaperAuthorAffiliationRelationship.tsv`

| PaperId     |  AuthorId   |   AffiliationId   | AuthorSequenceNumber |
|-------------|-------------|-------------------|----------------------|
| 15120102    | 1972291593  |   118347636       |          3           |
| 23208396    | 707981970   |   99464096        |          1           |
| ....        | ....        | ....              | ....                 |


`Venue.tsv`

| VenueId  |       VenueShortName      |      VenueName          |
|----------|---------------------------|-------------------------|
| 61661    | journal of prosthodontics |Journal of Prosthodontics|
| 2622674682  |     AICT      |      International Conference on Application of Information and Communication Technologies        |
| ....  |     ....      |     ....       |


`PaperFieldOfStudyRelationship.tsv`

| PaperId    |  FieldOfStudyId            |
| -----------|----------------------------|
|   320896   |         206384180          |
|   563542   |      542774811             |
| ....       | ....                       |


`FieldOfStudy.tsv`

| FieldOfStudyId |  FieldLevel |          FieldName              |
|----------------|-------------|---------------------------------|
|   12843        |      2      |     gravitational singularity   |
|    4250        |      3      |      sign function              |
| ....           | ....        |     ....               |


### OrganizationInsight.pbit

The template visualizes the results using various charts and dynamic calculations. Each report page have input/output formatted as shown below:
![](/images/OrgInsight_Input_Output.png "Organization Insight Input/output") 

 
#### Template Parameters
| Parameter Name |  Type  |                  Description                  |
|----------------|--------|-----------------------------------------------|
|  ADL URI    | string | The URI of the Azure Data Lake Store where the script wrote its output. You can find this information through Azure Portal by navigating to [{Your data lake store instance}] -> [Overview] -> [Essentials]  |


### OrganizationInsight.pbix

This Power BI report file is for comparison. If you run the script as is then use OrganizationInsight.pbit to create a Power BI report, the visualization and interaction should be indentical. 

## Resources

- [Analytics & Visualization Samples for Academic Graph](https://github.com/Azure-Samples/academic-knowledge-analytics-visualization)
- [Microsoft Academic Website](https://academic.microsoft.com/)