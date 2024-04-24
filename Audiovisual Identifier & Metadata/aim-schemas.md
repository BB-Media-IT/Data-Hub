# Audiovisual Identifier & Metadata

This document details the schemas used to manage the `Audiovisual Identifier & Metadata` product data. During the delivery process, a specific S3 Bucket is created for each client. In each of these buckets, we have a main folder containing files in JSONL format. This folder is named `Sources`. Additionally, within this folder, there is a subfolder named `latest`, where the latest snapshot of the `Metadata BB` database is stored.

## Document Structure
This document is organized into the following sections:

- [**File Description**](#file-description)
- [**Table Visualization & Data Relationships**](#table-visualization--data-relationships)

## Details of the S3 Buckets
Each client receives an S3 Bucket where data is organized into specific folders to ensure efficient management and quick access. The folder names reflect the types of data they contain, facilitating the identification and specific processing of each data set:

#### Example: 
- `s3://bucket-client/Sources`

This folder contains a `latest` subfolder, which is periodically updated with the latest available snapshot, ensuring that customers always have access to the latest information.

#### Update frequency and scope
- The update of data in S3 Bucket is daily. 
- The scope is defined according to the needs of each client, guaranteeing at least `Metadata BB`.

🚀 You can get a weekly updated demo by connecting to the following Bucket `s3://bb-media-data/audiovisual-identifier-and-metadata/` using AWS CLI or any software and the endpoint parameter `--endpoint https://nyc3.digitaloceanspaces.com`.

>**Command example** `aws s3 --endpoint https://nyc3.digitaloceanspaces.com cp s3://bb-media-data/audiovisual-identifier-and-metadata/ /Demo/BB-Media --recursive`

## File Description
We provide a detailed description of the files contained in the `Sources` folder, explaining the structure and type of data handled by each one. If you wish to see the schemas in YAML, [click here](schemas-yml).

### BBIDs
| Field        | Type   | Description                                                               | Example                          |
|--------------|--------|---------------------------------------------------------------------------|----------------------------------|
| UID          | string | The ID created by BB which identifies a group of external IDs.            | a646fad6731af909f1a7d4309c2cd069 |
| ExternalIds  | array  | -                                                                         | [View More In ExternalIds](#externalids) |

#### ExternalIds
| Field      | Type   | Description                                                   | Example                        |
|------------|--------|---------------------------------------------------------------|--------------------------------|
| UID        | string | The ID created by BB which identifies a group of external IDs.| a646fad6731af909f1a7d4309c2cd069 |
| Provider   | string | Identifies the source of the ID.                              |                                |
| ID         | string | The ID from the external provider.                            |                                |
| Type       | string | The type assigned by the external provider.                   |                                |
| CreatedAt  | string | The time when the ID was inserted in our database.            | 2017-07-21T17:32:28+00:00 |
| UpdatedAt  | string | The time when the ID was last updated in our database.        | 2017-07-21T17:32:28+00:00 |

### SourcesContents

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| UID | string | Universal BB ID. |  |
| Source | string | Source of the metadata. |  |
| Id | string | ID in the external database. | tt13443470 |
| Title | string |  |  |
| OriginalTitle | string |  |  |
| Year | integer |  |  |
| Directors | array |  |  |
| CreatedBy | array |  |  |
| Cast | array |  |  |
| Crew | array |  | [View More In Crew](#Crew) |
| Akas | array |  | [View More In Akas](#Akas) |
| Country | array | List of production countries. |  |
| Companies | array |  | [View More In Companies](#Companies) |
| Synopsis | array |  | [View More In Synopsis](#Synopsis) |
| Images | array |  | [View More In Images](#Images) |
| Videos | array | Trailers or other promotional videos. | [View More In Videos](#Videos) |
| Languages | array |  |  |
| ReleaseYears | array | List of release years by territory. | [View More In ReleaseYears](#ReleaseYears) |
| ReleaseDate | string |  |  |
| Duration | integer |  |  |
| Genres | array |  |  |
| Homepage | string |  |  |
| Keywords | array |  |  |
| Status | string |  |  |
| Type | string |  |  |
| IsAdult | boolean |  |  |
| Franchise | string |  |  |
| Scripted | boolean |  |  |
| Seasons | array |  | [View More In Seasons](#Seasons) |
| Rating | array | Age rating. |  |
| CreatedAt | string | Indicates when the record was created in our database. | 2017-07-21 17:32:28+00:00 |
| UpdatedAt | string | Indicates when the record was updated in our database. | 2017-07-21 17:32:28+00:00 |

#### Crew
| Field | Type | Description | Example |
| --- | --- | --- | --- |
| Name | string |  |  |
| Role | string |  |  |
#### Akas
| Field | Type | Description | Example |
| --- | --- | --- | --- |
| Language | string |  |  |
| Region | string |  |  |
| Title | string |  |  |
#### Companies
| Field | Type | Description | Example |
| --- | --- | --- | --- |
| Country | string |  |  |
| Name | string |  |  |
| Type | string |  |  |
#### Synopsis
| Field | Type | Description | Example |
| --- | --- | --- | --- |
| Region | string |  |  |
| Language | string |  |  |
| Description | string |  |  |
#### Images
| Field | Type | Description | Example |
| --- | --- | --- | --- |
| Type | string |  |  |
| Language | string |  |  |
| URL | string |  |  |
| BBURL | string |  |  |
#### Videos
| Field | Type | Description | Example |
| --- | --- | --- | --- |
| Provider | string |  |  |
| Id | string |  |  |
| Language | string |  |  |
| Type | string |  |  |
#### ReleaseYears
| Field | Type | Description | Example |
| --- | --- | --- | --- |
| Country | string |  |  |
| Year | integer |  |  |
#### Seasons
| Field | Type | Description | Example |
| --- | --- | --- | --- |
| Number | integer | Season number. |  |
| Episodes | integer | Number of episodes in the season. |  |
| Year | integer |  |  |
| SeasonId | integer |  |  |
| Title | string |  |  |


### SourcesImages
| Field      | Type   | Description                                            | Example                          |
|------------|--------|--------------------------------------------------------|----------------------------------|
| UID        | string | Content ID by BB.                                      | a646fad6731af909f1a7d4309c2cd069 |
| ID         | string | Content ID determined by the provider.                 |                                  |
| Type       | string | Content type determined by the provider.               |                                  |
| Provider   | string | Identifies where the images were sourced.              |                                  |
| Images     | array  | -                                                      | [View More In Images](#images)   |
| Seasons    | array  | -                                                      | [View More In Seasons](#seasons) |
| CreatedAt  | string | Indicates when the record was created in our database. | 2017-07-21T17:32:28Z             |

#### Images
| Field    | Type   | Description | Example |
|----------|--------|-------------|---------|
| Type     | string | -           |         |
| ImageUrl | string | -           |         |

#### Seasons
| Field    | Type   | Description   | Example                                         |
|----------|--------|---------------|-------------------------------------------------|
| ID       | string | -             |                                                 |
| Number   | integer| Season number.|                                                 |
| Images   | array  | -             | [View More In Season Images](#season-images)    |
| Episodes | array  | -             | [View More In Episodes](#episodes)              |

#### Season Images
| Field    | Type   | Description | Example |
|----------|--------|-------------|---------|
| Type     | string | -           |         |
| ImageUrl | string | -           |         |

#### Episodes
| Field    | Type   | Description   | Example                                       |
|----------|--------|---------------|-----------------------------------------------|
| ID       | integer| -             |                                               |
| Number   | integer| Episode number|                                               |
| Images   | array  | -             | [View More In Episode Images](#episode-images)|

#### Episode Images
| Field    | Type   | Description | Example |
|----------|--------|-------------|---------|
| Type     | string | -           |         |
| ImageUrl | string | -           |         |

### SourcesPopularity
| Field           | Type    | Description                                            | Example                  |
|-----------------|---------|--------------------------------------------------------|--------------------------|
| UID             | string  | -                                                      | a646fad6731af909f1a7d4309c2cd069 |
| Provider        | string  | -                                                      |                          |
| ID              | string  | -                                                      |                          |
| Popularity      | integer | -                                                      |                          |
| MetacriticScore | integer | -                                                      |                          |
| CreatedAt       | string  | Indicates when the record was created in our database. | 2017-07-21T17:32:28Z     |

### SourcesRatings
| Field     | Type    | Description                                            | Example                  |
|-----------|---------|--------------------------------------------------------|--------------------------|
| UID       | string  | -                                                      | a646fad6731af909f1a7d4309c2cd069 |
| Provider  | string  | -                                                      |                          |
| ID        | string  | -                                                      |                          |
| Votes     | integer | -                                                      |                          |
| Score     | number  | -                                                      |                          |
| CreatedAt | string  | Indicates when the record was created in our database. | 2017-07-21T17:32:28Z     |

## Table Visualization & Data Relationships
We include tables to clearly visualize the relationships and key fields in each JSONL file and analyze how the various files interrelate to provide a complete view of the overall `Audiovisual Identifier & Metadata` product data model.

You can obtain the relationships between all BB Media products in this [link](/File%20Relationships/relationships.md).


>👋 For more information and pricing details, please feel free to [click here](mailto:hello@bb-media.com?subject=Let's%20Unlock%20Amazing%20Deals%20Together!)! We'd love to help you.