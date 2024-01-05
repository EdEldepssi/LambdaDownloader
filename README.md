# AWS Lambda ETL Process Overview

## Introduction
This document outlines the ETL (Extract, Transform, Load) process designed to run on AWS Lambda. The process involves several steps to download, process, and upload files to an AWS S3 bucket.

## Process Steps

1. **Configuration Retrieval**: 
    - Retrieves S3 bucket name, bookmark file name, baseline file name, and file prefix from environment variables.

2. **File Processing Loop**:
   - **Previous File Identification**: Uses `get_prev_file_name` from `util.py` to find the name of the previously processed file. Uses a baseline file if none is found.
   - **Next File Generation**: Predicts the name of the next file to process using `get_next_file_name` from `util.py`.
   - **File Downloading**: Attempts to download the next file. If the file doesn't exist (404 status), the process is assumed to be caught up and the loop breaks.
   - **File Upload to S3**: Uploads the successfully downloaded file to an S3 bucket.
   - **Bookmark Updating**: Updates the bookmark file with the name of the last processed file using `upload_bookmark` from `util.py`.

3. **Validation**: 
    - `lambda_validate.py` script invokes `lambda_handler` from `lambda_function.py` and prints the result.

## Technologies and Libraries Used

- **AWS Lambda**: Serverless computing platform.
- **AWS S3**: Object storage service.
- **Boto3**: AWS SDK for Python, for interacting with AWS services.
- **Requests**: Library for making HTTP requests.
- **OS**: Standard Python library for OS interaction.
- **Datetime**: Standard Python library for date and time manipulation.

