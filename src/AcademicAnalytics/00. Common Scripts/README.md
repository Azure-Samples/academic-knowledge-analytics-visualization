# CreateDatabase.usql

This script creats a USQL database using same schema as the graph text files and indexes the id columns.

## Data Schema

> Note: &quot;Rank&quot; values in the entity files are the log probability of an entity being important multiplied by a constant(-1000).
>Rank = -1000 \* Ln( probability of an entity being important )

## Affiliations.txt

Column # | Name | Type | Note
--- | --- | --- | ---
1 | AffiliationId | long | PRIMARY KEY
2 | Rank | uint |
3 | NormalizedName | string |
4 | DisplayName | string |
5 | GridId | string |
6 | OfficialPage | string |
7 | WikiPage | string |
8 | PaperCount | long |
9 | CitationCount | long |
10 | CreatedDate | DateTime |

## Authors.txt

Column # | Name | Type | Note
--- | --- | --- | ---
1 | AuthorId | long | PRIMARY KEY
2 | Rank | uint |
3 | NormalizedName | string |
4 | DisplayName | string |
5 | LastKnownAffiliationId | long? |
6 | PaperCount | long |
7 | CitationCount | long |
8 | CreatedDate | DateTime |

## ConferenceInstances.txt

Column # | Name | Type | Note
--- | --- | --- | ---
1 | ConferenceInstanceId | long | PRIMARY KEY
2 | NormalizedName | string |
3 | DisplayName | string |
4 | ConferenceSeriesId | long | FOREIGN KEY REFERENCES ConferenceSeries(ConferenceSeriesId)
5 | Location | string |
6 | OfficialUrl | string |
7 | StartDate | DateTime? |
8 | EndDate | DateTime? |
9 | AbstractRegistrationDate | DateTime? |
10 | SubmissionDeadlineDate | DateTime? |
11 | NotificationDueDate | DateTime? |
12 | FinalVersionDueDate | DateTime? |
13 | PaperCount | long |
14 | CitationCount | long |
15 | CreatedDate | DateTime |

## ConferenceSeries.txt

Column # | Name | Type | Note
--- | --- | --- | ---
1 | ConferenceSeriesId | long | PRIMARY KEY
2 | Rank | uint |
3 | NormalizedName | string |
4 | DisplayName | string |
5 | PaperCount | long |
6 | CitationCount | long |
7 | CreatedDate | DateTime |

## FieldsOfStudyChildren.txt

Column # | Name | Type | Note
--- | --- | --- | ---
1 | FieldOfStudyId | long | FOREIGN KEY REFERENCES FieldsOfStudy(FieldOfStudyId)
2 | ChildFieldOfStudyId | long | FOREIGN KEY REFERENCES FieldsOfStudy(FieldOfStudyId)

## FieldsOfStudy.txt

Column # | Name | Type | Note
--- | --- | --- | ---
1 | FieldOfStudyId | long | PRIMARY KEY
2 | Rank | uint |
3 | NormalizedName | string |
4 | DisplayName | string |
5 | MainType | string |
6 | Level | Int | 0 - 5
7 | PaperCount | long |
8 | CitationCount | long |
9 | CreatedDate | DateTime |

## Journals.txt

Column # | Name | Type | Note
--- | --- | --- | ---
1 | JournalId| long | PRIMARY KEY
2 | Rank | uint |
3 | NormalizedName | string |
4 | DisplayName | string |
5 | Issn | string |
6 | Publisher | string |
7 | Webpage | string |
8 | PaperCount | long |
9 | CitationCount | long |
10 | CreatedDate | DateTime |

## PaperAbstractInvertedIndex.txt

Column # | Name | Type | Note
--- | --- | --- | ---
1 | PaperId | long | FOREIGN KEY REFERENCES Papers(PaperId)
2 | IndexedAbstract | string | See [Microsoft Academic Graph FAQ](resources-faq)

## PaperAuthorAffiliations.txt

Column # | Name | Type | Note
--- | --- | --- | ---
1 | PaperId | long | FOREIGN KEY REFERENCES Papers(PaperId)
2 | AuthorId | long | FOREIGN KEY REFERENCES Authors(AuthorId)
3 | AffiliationId | long? | FOREIGN KEY REFERENCES Affiliations(AffiliationId)
4 | AuthorSequenceNumber | uint | 1-based author sequence number. 1: the 1st author listed on paper.
5 | OriginalAffiliation | string |

> [!NOTE]
> It is possible to have multiple rows with same (PaperId, AuthorId, AffiliationId) when an author is associated with multiple affiliations.

## PaperCitationContexts.txt

Column # | Name | Type | Note
--- | --- | --- | ---
1 | PaperId | long | FOREIGN KEY REFERENCES Papers(PaperId)
2 | PaperReferenceId | long | FOREIGN KEY REFERENCES Papers(PaperId)
3 | CitationContext | string |

## PaperFieldsOfStudy.txt

Column # | Name | Type | Note
--- | --- | --- | ---
1 | PaperId | long | FOREIGN KEY REFERENCES Papers(PaperId)
2 | FieldOfStudyId | long | FOREIGN KEY REFERENCES FieldsOfStudy(FieldOfStudyId)
3 | Score | float | Confidence range between 0 and 1. Bigger number representing higher confidence.

## PaperLanguages.txt

Column # | Name | Type | Note
--- | --- | --- | ---
1 | PaperId | long | FOREIGN KEY REFERENCES Papers(PaperId)
2 | LanguageCode | string |

## PaperRecommendations.txt

Column # | Name | Type | Note
--- | --- | --- | ---
1 | PaperId | long | FOREIGN KEY REFERENCES Papers(PaperId)
2 | RecommendedPaperId | long | FOREIGN KEY REFERENCES Papers(PaperId)
3 | Score | float | Confidence range between 0 and 1. Bigger number representing higher confidence.

## PaperReferences.txt

Column # | Name | Type | Note
--- | --- | --- | ---
1 | PaperId | long | FOREIGN KEY REFERENCES Papers(PaperId)
2 | PaperReferenceId | long | FOREIGN KEY REFERENCES Papers(PaperId)

## PaperResources.txt

Column # | Name | Type | Note
--- | --- | --- | ---
1 | PaperId | long | FOREIGN KEY REFERENCES Papers(PaperId)
2 | ResourceType | int |
3 | ResourceUrl | string | Bit flags. 1 = Project, 2 = Data, 4 = Code
4 | SourceUrl | string |
5 | RelationshipType | int | Bit flags. 1 = Own, 2 = Cite

## PaperUrls.txt

Column # | Name | Type | Note
--- | --- | --- | ---
1 | PaperId | long | FOREIGN KEY REFERENCES Papers(PaperId)
2 | SourceType | int? |
3 | SourceUrl | string |

## Papers.txt

Column # | Name | Type | Note
--- | --- | --- | ---
1 | PaperId | long | PRIMARY KEY
2 | Rank | uint |
3 | Doi | string |
4 | DocType | string | Book, BookChapter, Conference, Journal, Patent, NULL : unknown
5 | PaperTitle | string |
6 | OriginalTitle | string |
7 | BookTitle | string |
8 | Year | int |
9 | Date | DateTime? |
10 | Publisher | string |
11 | JournalId | long? | FOREIGN KEY REFERENCES Journals(JournalId)
12 | ConferenceSeriesId | long? | FOREIGN KEY REFERENCES ConferenceSeries(ConferenceSeriesId)
13 | ConferenceInstanceId | long? | FOREIGN KEY REFERENCES ConferenceInstances(ConferenceInstanceId)
14 | Volume | string |
15 | Issue | string |
16 | FirstPage | string |
17 | LastPage | string |
18 | ReferenceCount | long |
19 | CitationCount | long |
20 | EstimatedCitationCount | long |
21 | OriginalVenue | string |
22 | CreatedDate | DateTime |

## RelatedFieldOfStudy.txt

Column # | Name | Type | Note
--- | --- | --- | ---
1 | FieldOfStudyId1 | long | FOREIGN KEY REFERENCES FieldsOfStudy(FieldOfStudyId)
2 | Type1 | string | disease, disease_cause, medical_treatment, symptom
3 | FieldOfStudyId2 | long | FOREIGN KEY REFERENCES FieldsOfStudy(FieldOfStudyId)
4 | Type2 | string | disease, disease_cause, medical_treatment, symptom
5 | Rank | float | Confidence range between 0 and 1. Bigger number representing higher confidence.