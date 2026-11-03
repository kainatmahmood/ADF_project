# Azure Data Factory – Data Engineering Project

## Project Overview

This project focuses on building and managing data integration workflows using Microsoft Azure Data Factory (ADF). It covers different ETL processes, including data extraction from SQL databases and REST APIs, data movement to Azure Storage, incremental data loading, and pipeline monitoring.

The project also explores how different Azure Data Factory components work together to automate data workflows.

## Technologies Used

- Microsoft Azure
- Azure Data Factory (ADF)
- Azure SQL Database
- Azure Data Lake Storage Gen2
- Azure Logic Apps
- REST APIs
- SQL
- JSON
- GitHub

## Project Architecture

The project follows a basic data integration workflow:

```text
Source Systems
     |
     |-- SQL Database
     |
     |-- REST APIs
     |
     v
Azure Data Factory
     |
     |-- Data Extraction
     |-- Data Transformation
     |-- Incremental Loading
     |-- Pipeline Orchestration
     |
     v
Azure Storage
     |
     v
Data Files (CSV / JSON)
     |
     v
Pipeline Monitoring
     |
     v
Azure Logic Apps
     |
     v
Email Notifications
```

## Pipelines and Their Purpose

### 1. Incremental Data Load Pipeline

This pipeline demonstrates incremental data loading from a SQL database to Azure Storage.

Instead of copying the entire dataset every time, it identifies and loads only new or updated records using a watermark column (`last_updated`).

**Key Activities:**
- Lookup: Retrieves the previously stored watermark timestamp.
- Lookup: Checks whether new or updated records are available.
- If Condition: Determines whether records need to be processed.
- Copy Data: Transfers new or updated records to the destination.
- Lookup: Retrieves the latest update timestamp.
- Watermark Update: Stores the latest timestamp for the next pipeline execution.

**Purpose:** To reduce unnecessary data transfers and make data ingestion more efficient.

### 2. REST API Data Extraction Pipeline

This pipeline demonstrates how to extract data from REST APIs and store the API response in Azure Storage.

It uses Azure Data Factory's REST connector to retrieve data from an API endpoint.

**Key Activities:**
- Web Activity: Retrieves information from the API endpoint when required.
- Copy Data: Extracts API data and transfers it to the destination.
- Pagination: Uses parameters such as `limit` and `offset` to retrieve records in batches.

**Purpose:** To understand API-based data ingestion and handle large datasets through pagination.

### 3. File Processing Pipeline

This pipeline demonstrates how to process multiple files stored in Azure Storage.

It uses dynamic expressions and conditional logic to handle files during pipeline execution.

**Key Activities:**
- Get Metadata: Retrieves information about files.
- ForEach: Iterates through the available files.
- If Condition: Applies conditions to control file processing.
- Copy Data: Moves the selected files to the destination.

**Purpose:** To automate file processing and understand dynamic pipeline execution.

### 4. Pipeline Monitoring and Email Notifications

This workflow demonstrates how Azure Data Factory can work with Azure Logic Apps to generate email notifications.

When a pipeline execution completes, its status can be used to trigger a notification workflow.

**Key Activities:**
- Azure Data Factory: Executes the data pipeline.
- Logic Apps: Handles the notification workflow.
- Email Connector: Sends an email notification to the configured recipient.

**Purpose:** To understand pipeline monitoring and automated failure or success notifications.

## Azure Data Factory Components

The repository contains the following ADF resource configurations:

| Component | Description |
|---|---|
| Pipelines | Define and orchestrate data integration workflows. |
| Datasets | Represent the structure and location of source and destination data. |
| Linked Services | Define connections to data sources and destinations. |
| Data Flows | Define data transformation operations. |
| Integration Runtime | Provides the infrastructure for data movement and activity execution. |
| Factory | Contains the Data Factory resource configuration. |

## Repository Structure

```text
ADF_project/
│
├── dataflow/
│
├── dataset/
│
├── factory/
│
├── integrationRuntime/
│
├── linkedService/
│
├── pipeline/
│
├── publish_config.json
│
└── README.md
```

## Key Learning Outcomes

Through this project, I have gained practical experience in:

- Building and managing ETL pipelines using Azure Data Factory.
- Connecting SQL databases and REST APIs with Azure Data Factory.
- Moving data between source systems and Azure Storage.
- Implementing incremental data loading using watermark timestamps.
- Working with API pagination and dynamic parameters.
- Processing multiple files using ForEach and If Condition activities.
- Understanding data transformation and pipeline orchestration.
- Integrating Azure Logic Apps for email notifications.
- Managing Data Factory resources using GitHub.

## Getting Started

To explore this project:

1. Clone the repository:

   ```bash
   git clone https://github.com/kainatmahmood/ADF_project.git
   ```

2. Open the repository in your preferred code editor.
3. Review the pipeline, dataset, and linked service configurations.
4. Open Azure Data Factory Studio.
5. Configure the required Azure resources and linked services.
6. Update connection details according to your environment.
7. Validate and execute the pipelines.

**Note:** Azure resources and connection configurations must be set up before executing the pipelines.

## Author

**Kainat Mahmood**

GitHub: https://github.com/kainatmahmood

