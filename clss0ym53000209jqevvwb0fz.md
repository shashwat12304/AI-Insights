---
title: "Document AI REST API || Google Cloud"
datePublished: Sun Feb 18 2024 21:33:39 GMT+0000 (Coordinated Universal Time)
cuid: clss0ym53000209jqevvwb0fz
slug: document-ai-rest-api-google-cloud
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1708282655422/95b14d23-e51a-4562-9825-eaf2536d04dc.jpeg
tags: artificial-intelligence, json, google-cloud, command-line, google-cloud-platform, deep-learning, mlops, document-ai

---

# Introduction

## What is Document AI?

Google Cloud Document AI empowers organizations to unlock the value hidden within their unstructured documents. It leverages pre-trained machine learning models to extract, classify, and structure information from various document types, including invoices, receipts, contracts, and forms. For organizations grappling with an ever-growing volume of unstructured documents, it offers a powerful solution to unlock hidden data and gain valuable insights, driving efficiency and informed decision-making.

## Key Features

1. **Automated Information Extraction:** Extract text, key-value pairs, entities, and tables from diverse document formats (PDF, scans, images).
    
2. **Efficient Task Automation:** Streamline workflows by automating tedious manual tasks like data entry and document classification.
    
3. **Customizable Model Development:** Train and deploy custom models tailored to specific document types and information needs.
    
4. **Integrated Cloud Environment:** Seamlessly connect Document AI with other Google Cloud services for holistic data processing and analysis.
    
5. **Enhanced Accuracy and Scalability:** Benefit from pre-trained models and fine-tuning capabilities for high-precision document understanding.
    

## Scope of this blog

This blog acts as an in-depth guide on interacting with the Document AI REST API using the curl command-line tool, addressing the potential errors and difficulties and streamlining the process for you when you try it for the first time. I will also cover other aspects and details of Document AI in my future blogs. You can refer to the official Document AI documentation for further details:

[Official Document AI GCP documentation](https://cloud.google.com/document-ai?hl=en)

# Prerequisites

1. Curl installed
    
2. Google Cloud Platform project with Document AI-enabled
    
3. Service account with Document AI User role
    

# Step-by-Step Guide

## Authentication

1. Initialize gcloud CLI:
    
    ```bash
    gcloud init
    ```
    
2. Obtain an access token:
    

```bash
gcloud auth application-default print-access-token
```

Save this access token for later use.

## Constructing the command

* The basic structure remains:
    
    ```bash
    curl -X POST -H "Authorization: Bearer <access_token>" -H 
    "Content-Type: application/json" -d @<input_file.json> -o 
    <output_file.json> <prediction_endpoint>
    ```
    
* Remember to replace placeholders with your specific details.
    

## Creating a General Purpose Processor

1. In the Google Cloud Console, navigate to the Document AI section.
    
2. Click on the Explore processors button.
    
3. Click on Create Processor and select Form Parser as the processor type.
    
4. Give your processor a name and select a region.
    
5. Click Create to create the processor.
    
6. Once created, go to the Overview tab and copy the Prediction Endpoint for your new processor.
    

## Obtaining the Prediction Endpoint

1. Open the Google Cloud Console and navigate to the Document AI section.
    
2. Select the Processors tab.
    
3. Click on the name of the General Purpose Processor you want to use.
    
4. In the Overview tab, copy the Prediction Endpoint listed under API details. This is what you need in your curl command.
    

## Input File Structure

* The input\_file.json format stays the same as follows:
    
    ```json
    {
         "inlineDocument": {
         "mimeType": "<mime_type>",
         "content": "<base64_encoded_content>"
         }
    }
    ```
    

Ensure matches supported formats **<mark>(PDF, GIF, TIFF, JPEG, PNG, BMP, WEBP.</mark>**

## Encoding the content securely

1. Prefer not to use online base64 converters due to potential security risks and processing issues.
    
2. Encode content locally using platform-specific methods:
    
    **Windows**
    
    *Powershell*
    
    ```bash
    $pdfBytes = [System.IO.File]::ReadAllBytes("<path_to_pdf>")
    ```
    
    ```bash
    $base64String = [System.Convert]::ToBase64String($pdfBytes)
    ```
    
    ```bash
    echo $base64String > test.txt
    ```
    
    **Linux/Mac OS**
    
    *Bash*
    
    ```bash
    base64 <path_to_pdf> > test.txt
    ```
    
3. Extract the base64 string from test.txt and put it in the content field of input\_file.json.
    

## Executing the command

1. Navigate to the directory containing input\_file.json and output\_file.json.
    
2. Run the curl command with your specific details.
    

The extracted information will be saved in output\_file.json.

# Troubleshooting

### *<mark>401</mark> Authentication Error*

Double-check access token validity and service account's Document AI User role.

### *Mime Type Not Acceptable*

Confirm your document type matches supported formats.

### *Invalid Content Input*

Always use local encoding methods mentioned above instead of using avoiding online converters.

# Beyond Basics

## Supported features

Explore the Document AI API documentation for details on:

* Supported processors and their functionalities.
    
* Extractable information types (e.g., text, entities, tables).
    
* Language support for different processors
    
* Tailor your curl commands to extract specific information based on your processor's capabilities.
    

## Environment Variables

* Consider using environment variables for sensitive information like access tokens to enhance security and manage multiple accounts effectively.
    

Tools like <mark>dotenv </mark> can simplify environment variable usage in shell scripts.

## Error Handling

* Incorporate error-handling mechanisms in your curl commands to gracefully handle potential issues like network failures or API errors.
    
* Utilize curl exit codes and conditionals to provide informative feedback to the user.
    

Refer to the official Document AI API documentation for a comprehensive understanding of advanced features and functionalities. This guide provides a solid foundation, but continuous exploration of the API opens up wider possibilities for document processing automation. This enhanced guide empowers you with deeper insights and best practices for using the Document AI REST API effectively via curl.

**Thanks for reading :)**