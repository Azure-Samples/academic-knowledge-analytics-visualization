---
title: Analytics and Visualization Samples for Academic Graph
services: academic-knowledge
platforms: dotnet
author: alch-msft
ms.topic: tutorial
ms.service: data-lake-analytics
description: This project illustrates how to perform analystics and visualization for Microsoft Academic Graph using Data Lake Analytics (USQL) and Power BI.
---

# Analytics & Visualization Samples for Academic Graph 

This project aims to help data scientists become familar with the Microsoft Academic Graph through analystics and visualization samples using Data Lake Analytics (USQL) and Power BI.  

## Samples

The project contains 13 samples 

* [Field of Study Top Authors](https://github.com/Azure-Samples/academic-knowledge-analytics-visualization/tree/master/src/AcademicAnalytics/01.%20Field%20of%20Study%20Top%20Authors)
* [Field of Study Entity Counts](https://github.com/Azure-Samples/academic-knowledge-analytics-visualization/tree/master/src/AcademicAnalytics/11.%20Field%20of%20Study%20Entity%20Counts)
* [Field of Study Top Entities](https://github.com/Azure-Samples/academic-knowledge-analytics-visualization/tree/master/src/AcademicAnalytics/13.%20Field%20of%20Study%20Top%20Entities)
* [Conference Top Authors By Static Rank](https://github.com/Azure-Samples/academic-knowledge-analytics-visualization/tree/master/src/AcademicAnalytics/02.%20Conference%20Top%20Authors%20By%20Static%20Rank)
* [Conference Paper Statistics](https://github.com/Azure-Samples/academic-knowledge-analytics-visualization/tree/master/src/AcademicAnalytics/03.%20Conference%20Papers%20Basic%20Statistics)
* [Conference Top Papers](https://github.com/Azure-Samples/academic-knowledge-analytics-visualization/tree/master/src/AcademicAnalytics/04.%20Conference%20Top%20Papers)
* [Conference Top Authors](https://github.com/Azure-Samples/academic-knowledge-analytics-visualization/tree/master/src/AcademicAnalytics/05.%20Conference%20Top%20Authors)
* [Conference Top Institutions](https://github.com/Azure-Samples/academic-knowledge-analytics-visualization/tree/master/src/AcademicAnalytics/06.%20Conference%20Top%20Institutions)
* [Conference Memory of References](https://github.com/Azure-Samples/academic-knowledge-analytics-visualization/tree/master/src/AcademicAnalytics/07.%20Conference%20Memory%20of%20References)
* [Conference Top Referenced Venues](https://github.com/Azure-Samples/academic-knowledge-analytics-visualization/tree/master/src/AcademicAnalytics/08.%20Conference%20Top%20Referenced%20Venues)
* [Conference Top Citing Venues](https://github.com/Azure-Samples/academic-knowledge-analytics-visualization/tree/master/src/AcademicAnalytics/09.%20Conference%20Top%20Citing%20Venues)
* [Conference Tredning Topics](https://github.com/Azure-Samples/academic-knowledge-analytics-visualization/tree/master/src/AcademicAnalytics/10.%20Conference%20Trending%20Topics)
* [Organization Insight](https://github.com/Azure-Samples/academic-knowledge-analytics-visualization/tree/master/src/AcademicAnalytics/12.%20Organization%20Insight)


## Getting Started

### Pre-requisites

* [Get Microsoft Academic Graph on Azure Storage](https://docs.microsoft.com/en-us/academic-services/graph/get-started-setup-provisioning)
* [Set up Azure Data Lake Analytics for Microsoft Academic Graph](https://docs.microsoft.com/en-us/academic-services/graph/get-started-setup-azure-data-lake-analytics)
* [Microsoft Power BI Desktop client](https://powerbi.microsoft.com/en-us/desktop/)
* Visual Studio 2017 or Visual Studio 2015 with [Data Lake tools](https://www.microsoft.com/en-us/download/details.aspx?id=49504)

### Quickstart

### Gather the information that you need

   Before you begin, you should have these items of information:

   :heavy_check_mark:  The name of your Azure Storage (AS) account containing MAG dataset from [Get Microsoft Academic Graph on Azure storage](get-started-setup-provisioning.md#note-azure-storage-account-name-and-primary-key).

   :heavy_check_mark:  The name of your Azure Data Lake Analytics (ADLA) service from [Set up Azure Data Lake Analytics](get-started-setup-azure-data-lake-analytics.md#create-azure-data-lake-analytics-account).

   :heavy_check_mark:  The name of your Azure Data Lake Storage (ADLS) from [Set up Azure Data Lake Analytics](get-started-setup-azure-data-lake-analytics.md#create-azure-data-lake-analytics-account).

   :heavy_check_mark:  The name of the container in your Azure Storage (AS) account containing MAG dataset.

### Create database from MAG data before running analytics examples

In prerequisite [Set up Azure Data Lake Analytics](get-started-setup-azure-data-lake-analytics.md), you added the Azure Storage  (AS) created for MAG provision as a data source for the Azure Data Lake Analytics service (ADLA). In this section, you submit an ADLA job to create database from MAG data.

1. In the [Azure portal](https://portal.azure.com), go to the Azure Data Lake Analytics (ADLA) service that you created, and select **Overview** > **New Job**.

   ![Azure Data Lake Analytics - New job](media/samples-azure-data-lake-hindex/new-job.png "Azure Data Lake Analytics - New job")

1. Copy code in samples/CreateDatabase.usql and paste into the code block.
   
1. Provide a **Job name** and select **Submit**.

   ![Submit CreateFunctions job](media/samples-azure-data-lake-hindex/create-functions-submit.png "Submit CreateFunctions job")

1. The job should finish successfully.

#### Running Example Analytics
1. Download or clone the repository.
2. Open the solution /src/AcademicAnalytics.sln
3. For each tutorial there should be: A USQL script(.usql), a Power BI report(.pbix), a Power BI template(.pbit) and a README explaining the tutorial. 
4. Althought each tutorial is different, running the USQL script as is and filling out the Power BI template using the same USQL parameters should give you a Power BI report with visualizations that match the Power BI report example included in the tutorial. Since the Microsoft Academic graph is contently improving, different graph verions may give you slightly different results.

#### Working with USQL scripts 
- How to run
    - Make sure you have selected your ADLA account


    ![Select your ADLA Account in Visual Studio](images/VSSelectADLAAccount.png)

    - Build the script first to validate syntax


    ![Build USQL script in Visual Studio](images/VSBuildScript.png)

    - Submit your script to your ADLA account


    ![Submit USCQL script in Visual Studio](images/VSSubmitScript.png)

- How to view the results
    - You can view the results via azure portal

    
    ![Azure Data lake Analyatics Data explorer](images/ADLADataExplorer.png)
    ![Azure Data lake Analyatics Data explorer2](images/ADLADataExplorer2.png)


#### Using Power BI 
- Make sure USQL script finished sucessfully
- Open up corresponding Power BI Template(.pbit) from file explorer (Visual studio doesn't recognize Power BI files) 
- Enter your ADL information and parameters corrisponding to your scripts
![Sample template load](/images/PBITemplateInitParam.png)
- Make sure the parameters cases are the same as your script and "click" to load

## Resources

- [Get started with Azure Data Lake Analytics using Azure portal](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal)
- [Develop USQL scripts by using Data Lake Tools for Visual Studio](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-data-lake-tools-get-started)
- [Get started with USQL](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-get-started)
- [Deep Dive into Query Parameters and Power BI Templates](https://powerbi.microsoft.com/en-us/blog/deep-dive-into-query-parameters-and-power-bi-templates/)
- [Manage Azure Data Lake Store resources by using Storage Explorer](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-in-storage-explorer)
- [Scalable Data Science with Azure Data Lake: An end-to-end Walkthrough](https://docs.microsoft.com/en-us/azure/machine-learning/team-data-science-process/data-lake-walkthrough)
- [Microsoft Academic Website](https://academic.microsoft.com/)