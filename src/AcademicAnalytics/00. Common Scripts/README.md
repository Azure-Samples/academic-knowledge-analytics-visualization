# CreateDatabase.usql

This script creats a USQL database using same schema as the graph text files and indexes the id columns.

## Data Schema

> Note: &quot;Rank&quot; values in the entity files are the log probability of an entity being important multiplied by a constant(-1000).
>Rank = -1000 \* Ln( probability of an entity being important )

`Affiliations.txt`

| **Description** | **Type** |
| --- | --- |
| Affiliation ID | long |
| Rank | uint |
| Normalized name | string |
| Display name | string |
| Paper count | long? |
| Citation count | long? |

`Authors.txt`

| **Description** | **Type** |
| --- | --- |
| Author ID | long |
| Rank | uint |
| Normalized name | string |
| Display name | string |
| Last known affiliation ID | long? |
| Paper count | long? |
| Citation count | long? |

`ConferenceInstances.txt`

| **Description** | **Type** |
| --- | --- |
| Conference instance ID | long |
| Rank | uint |
| Normalized name | string |
| Display name | string |
| Conference series ID | long? |
| Location | string |
| Official URL | string |
| Start date | DateTime? |
| End date | DateTime? |
| Abstract registration date | DateTime? |
| Submission deadline date | DateTime? |
| Notification due date | DateTime? |
| Final version due date | DateTime? |
| Paper count | long? |
| Citation count | long? |

`ConferenceSeries.txt`

| **Description** | **Type** |
| --- | --- |
| Conference series ID | long |
| Rank | uint |
| Normalized name | string |
| Display name | string |
| Paper count | long? |
| Citation count | long? |

`FieldsOfStudy.txt`

| **Description** | **Type** |
| --- | --- |
| Field of study ID | long |
| Rank | uint |
| Normalized name | string |
| Display name | string |
| Level | Int |
| Paper count | long? |
| Citation count | long? |

`FieldsOfStudyChildren.txt`

| **Description** | **Type** |
| --- | --- |
| Field of study ID | long |
| Child field of study ID | long |

`Journals.txt`

| **Description** | **Type** |
| --- | --- |
| Journal ID | long |
| Rank | uint |
| Normalized name | string |
| Display name | string |
| Paper count | long? |
| Citation count | long? |

`Papers.txt`

| **Description** | **Type** |
| --- | --- |
| Paper ID | long |
| Rank | uint |
| DOI | string |
| Doc type | string |
| Paper title | string |
| Original title | string |
| Book title | string |
| Year | int |
| Date | DateTimr? |
| Publisher | string |
| Journal ID | long? |
| Conference series ID | long? |
| Conference instance ID | long? |
| Volume | string |
| Issue | string |
| First page | string |
| Last page | string |
| Reference count | long |
| Citation count | long? |
| Estimated citation count | int? |

`PaperAbstractInvertedIndex.txt`

| **Description** | **Type** |
| --- | --- |
| Paper ID | long |
| Indexed abstract | string |

`PaperAuthorAffiliations.txt`

| **Description** | **Type** |
| --- | --- |
| Paper ID | long |
| Author ID | long |
| Affiliation ID | long? |
| Author sequence number | uint |

`PaperCitationContexts.txt`

| **Description** | **Type** |
| --- | --- |
| Paper ID | long |
| Paper reference ID | long |
| Citation context | string |

`PaperFieldsOfStudy.txt`

| **Description** | **Type** |
| --- | --- |
| Paper ID | long |
| Field of study ID | long |
| Similarity | float |

`PaperLanguages.txt`

| **Description** | **Type** |
| --- | --- |
| Paper ID | long |
| Language code | string |

`PaperReferences.txt`

| **Description** | **Type** |
| --- | --- |
| Paper ID | long |
| Paper reference ID | long |

`PaperUrls.txt`

| **Description** | **Type** |
| --- | --- |
| Paper ID | long |
| Source type | int? |
| Source URL | string |