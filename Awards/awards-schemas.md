# Awards

This document details the schemas used to manage the `Awards` product data. During the delivery process, a specific S3 Bucket is created for each client. In each of these buckets, we have a main folder containing files in JSONL format. This folder is named `Awards`. Additionally, within this folder, there is a subfolder named `latest`.

## Document Structure
This document is organized into the following sections:

- [**File Description**](#file-description)

## Details of the S3 Buckets
Each client receives an S3 Bucket where data is organized into specific folders to ensure efficient management and quick access. The folder names reflect the types of data they contain, facilitating the identification and specific processing of each data set:

#### Example: 
- `s3://bucket-client/Awards`

This folder contains a `latest` subfolder, which is periodically updated with the latest available snapshot, ensuring that customers always have access to the latest information.

#### Update frequency and scope
- The update of data in S3 Bucket is weekly. 

🚀 You can get a weekly updated demo by connecting to the following Bucket `s3://bb-media-data/awards/` using AWS CLI or any software and the endpoint parameter `--endpoint https://nyc3.digitaloceanspaces.com`.

>**Command example** `aws s3 --endpoint https://nyc3.digitaloceanspaces.com cp s3://bb-media-data/awards/ /Demo/BB-Media --recursive`

## File Description
We provide a detailed description of the files contained in the `Awards` folder, explaining the structure and type of data handled by each one. If you wish to see the schemas in YAML, [click here](schemas-yml).

### Awards
Field           | Type    | Description                                                    | Example 
----------------|---------|----------------------------------------------------------------|--- 
UID             | string  | The ID created by BB which identifies a group of external IDs. | f6343770f9212ebc396d74d21354ad33 
Event           | string  | No description provided. | 
Territory       | string  | No description provided. | 
Year            | integer | No description provided. | 
Category        | string  | No description provided. | 
Subcategory     | string  | No description provided. | 
WinnerOrNominee | string  | No description provided. | 
Title           | string  | No description provided. | 
EpisodeTitle    | string  | No description provided. | 
CotentType      | string  | No description provided. | 
ImdbIdContent   | string  | No description provided. | 
DataPerson      | array   | No description provided. | [View More In DataPerson](#dataperson)

#### DataPerson
Field  | Type   | Description              | Example 
-------|--------|--------------------------|--- 
Name   | string | No description provided. | 
ImdbId | string | No description provided. |  

>👋 For more information and pricing details, please feel free to [click here](mailto:hello@bb-media.com?subject=Let's%20Unlock%20Amazing%20Deals%20Together!)! We'd love to help you.
