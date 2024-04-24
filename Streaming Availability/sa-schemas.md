# Streaming Availability

This document details the schemas used to manage the data for the `Streaming Availability` product. During the delivery process, a specific S3 Bucket is generated for each client. In each of these buckets, we have three main folders that contain 
JSONL format files. These folders are organized as follows: `Contents`, `Episodes`, and `Stats`. Additionally, within each of these main folders, there is a subfolder called `latest`, where the latest snapshot from each streaming platform surveyed and 
contracted by the client is stored.

## Document Structure
This document is organized into the following sections:

- [**File Description**](#file-description)
- [**Table Visualization & Data Relationships**](#table-visualization--data-relationships)

## Details of the S3 Buckets
Each client receives an S3 Bucket where data is organized into specific folders to ensure efficient management and quick access. The folder names reflect the types of data they contain, facilitating the identification and specific processing of each data set:

#### Example: 
- `s3://bucket-client/Contents`
- `s3://bucket-client/Episodes`
- `s3://bucket-client/Stats`

Each of these folders contains a `latest` subfolder, which is periodically updated with the latest available snapshot, ensuring that clients always have access to the most recent information.

#### Update frequency and scope
- The update of the data in S3 Bucket is defined according to the needs of each customer.
- The scope is defined according to the needs of each customer.

🚀 You can get a weekly updated demo by connecting to the following Bucket `s3://bb-media-data/streaming-availability/` using AWS CLI or any software and the endpoint parameter `--endpoint https://nyc3.digitaloceanspaces.com`.

>**Command example** `aws s3 --endpoint https://nyc3.digitaloceanspaces.com cp s3://bb-media-data/streaming-availability/ /Demo/BB-Media --recursive`

## File Description
We provide a detailed description of the files contained in the `Contents`, `Episodes`, and `Stats` folders, explaining the structure and type of data each one manages. If you want to see the schemas in YAML, [click here](schemas-yml).

### Contents
| Field                 | Type     | Description                                                                                                  | Example                            |
|-----------------------|----------|--------------------------------------------------------------------------------------------------------------|------------------------------------|
| PlatformId            | integer  | ID for the platform.                                                                                         | 266                                |
| PlatformCode          | string   | Code identifying the platform and the territory.                                                             | us.disneyplus                      |
| PlatformName          | string   | Official name of the platform.                                                                               | Disney+                            |
| PlatformCountry       | string   | Country ISO 3166-1 alpha-2 code.                                                                             | US                                 |
| HashUnique            | string   | Hash identifying the movie or series in a specific platform and territory.                                   | ed3f48fd23236363df52e65b32c82e00   |
| UID                   | string   | Hash identifying the movie or series universally.                                                            | a646fad6731af909f1a7d4309c2cd069   |
| Id                    | string   | Identifier of the movie or series used in the platform itself.                                               | 498649d2-a45d-4d77-910c-f5fe1e837a90 |
| OtherIds              | array    | Only for Amazon platforms. The ASIN, GTI and CompactGTI IDs, when available.                                 | [view in OtherIds](#otherids)      |
| Title                 | string   | The title as it is found in the platform.                                                                    | Ant-Man and the Wasp: Quantumania  |
| CleanTitle            | string   | Title stripped of parentheses and other additions that don't belong to the title.                            | Ant-Man and the Wasp: Quantumania  |
| OriginalTitle         | string   | Title in the original language.                                                                              | `null`                             |
| Type                  | string   | The content type as it is assigned by the platform.                                                          | Movie, Tv Show                     |
| Year                  | integer  | The release year as it is listed by the platform.                                                            | 2023                               |
| Duration              | integer  | Runtime in minutes.                                                                                          | 127                                |
| ExternalIds           | array    | IDs from external databases that are mapped to the UID assigned to the movie or series.                      | [view in ExternalIds](#externalids)|
| Deeplinks             | object   | URLs pointing to the movie or series in the platform.                                                        | [view in Deeplinks](#deeplinks)    |
| PlaybackLink          | string   | URL that will immediately play the content on open.                                                          | https://www.disneyplus.com/video/498649d2-a45d-4d77-910c-f5fe1e837a90 |
| Synopsis              | string   | Description as found in the platform.                                                                        | Super Hero partners Scott Lang and Hope Van Dyne return to continue...   |
| Image                 | array    | Image URLs that point to the image assets found in the platform belonging to the movie or series.            | <image src="https://github.com/BB-Media-IT/Data-Hub/assets/4085605/3e0182ea-85d0-42ca-9bab-862ac2012dcf" height=100/> |
| Rating                | string   | Age rating information as found in the platform.                                                             | PG-13                              |
| Provider              | array    | Producer companies, if indicated by the platform.                                                            | `null`                             |
| Genres                | array    | Genres in English, parsed from the genres provided by the platform.                                          | ["Action","Adventure","Science Fiction"] |
| GenresPlatform        | array    | Genres as shown by the platform.                                                                             | ["Science Fiction","Superhero","Action-Adventure"] |
| Cast                  | array    | List of names from the cast, as provided by the platform.                                                    | ["Paul Rudd","Evangeline Lilly","Michael Douglas",...] |
| Crew                  | array    | List of crew members and their roles.                                                                        | [view in Crew](#crew)              |
| Directors             | array    | In the case of series, it may contain the series creators or episode directors.                              | ["Peyton Reed"]                    |
| Download              | boolean  | Indicates whether the content can be downloaded for offline watching.                                        | `true` `false` `null`              |
| IsOriginal            | boolean  | Whether the content is original to the platform.                                                             | `true` `false` `null`              |
| IsAdult               | boolean  | Whether the content is for adult audiences only.                                                             | `true` `false` `null`              |
| Packages              | array    | Business models available for the movie or series.                                                           | [view in Packages](#packages)      |
| CreatedAt             | string   | Indicates the time the data was scraped from the platform.                                                   | 2024-04-18T00:00:00Z               |
| IsBranded             | boolean  | Whether the content shows the platform branding.                                                             | `true` `false` `null`              |
| IsExclusive           | boolean  | Whether the content is exclusive to the platform.                                                            | `true` `false` `null`              |
| IsPremium             | boolean  | Whether the content requires an upgrade over the basic subscription.                                         | `true` `false` `null`              |
| Seasons               | array    | Information about seasons if applicable.                                                                     | [view in Seasons](#seasons)        |
| Subtitles             | array    | List of available subtitle languages as ISO 639-2 codes.                                                     | ["en","es","pt"]                   |
| Dubbed                | array    | List of available dub languages as ISO 639-2 codes.                                                          | ["en","es","pt"]                   |
| PopularityRankingBy   | array    | List of platform rankings and corresponding rank for the content.                                            | [view in PopularityRankingBy](#popularityrankingby)|
| UserData              | array    | List of attributes and values related to platform users, such as likes.                                      | [view in UserData](#userdata)      |

### Episodes
| Field             | Type    | Description                                                                                                                                                             | Example                             |
|-------------------|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------|
| PlatformId        | integer | ID for the platform. The ID refers to the platform across all available territories.                                                                                    | 34                                  |
| PlatformCode      | string  | Code identifying the platform and the territory.                                                                                                                        | ar.amazonprimevideo                 |
| PlatformName      | string  | Official name of the platform.                                                                                                                                          | Amazon Prime Video                  |
| PlatformCountry   | string  | Country ISO 3166-1 alpha-2 code.                                                                                                                                        | AR                                  |
| Season            | integer | Season number.                                                                                                                                                          | 1                                   |
| Episode           | integer | Episode number.                                                                                                                                                         | 8                                   |
| HashUnique        | string  | Hash identifying specific platform and territory.                                                                                                                       | cd33672d85f6eafb3e0f1b665882424a    |
| Id                | string  | Identifier of the episode used by the platform itself. If no ID is found in the platform, it may be the slug or a hash generated during the scraping of the data.       | amzn1.dv.gti.8276269a-402e-4ece-a2b0-4eb5e2504a05 |
| OtherIds          | array   | Only for Amazon platforms. The ASIN, GTI and CompactGTI IDs, when available.                                                                                            | [view in OtherIds](#otherids)       |
| ParentId          | string  | Identifier of the parent series used by the platform itself. If no ID is found in the platform, it may be the slug or a hash generated during the scraping of the data. | 0HAQAA7JM43QWX0H6GUD3IOF70          |
| ParentTitle       | string  | The title of the parent series as it is found in the platform.                                                                                                          | Fallout                             |
| ParentHashUnique  | string  | Hash identifying the parent series in a specific platform and territory.                                                                                                | cd7563ce07c1e2b4aa846d244acf0861    |
| ParentUID         | string  | Hash identifying the parent series universally.                                                                                                                         | 07a38fa2fa19b134ca248295e9976752    |
| Title             | string  | The episode title as it is found in the platform. If none is found, one is created using the 'Episode #' format.                                                        | El comienzo                         |
| OriginalTitle     | string  | Title in the original language.                                                                                                                                         | `null`                              |
| Type              | string  | Type of the content.                                                                                                                                                    | Episode                             |
| Year              | integer | Year of the episode.                                                                                                                                                    | 2024                                |
| Duration          | integer | Runtime in minutes.                                                                                                                                                     | 62                                  |
| ExternalIds       | array   | IDs from external databases that are mapped to the episode.                                                                                                             | [view in ExternalIds](#externalids) |
| Deeplinks         | object  | URLs pointing to the episode or season in the platform.                                                                                                                 | [view in Deeplinks](#deeplinks)     |
| PlaybackLink      | string  | Link to play the episode.                                                                                                                                               | https://primevideo.com/detail?gti=amzn1.dv.gti.8276269a-402e-4ece-a2b0-4eb5e2504a05&autoplay=1 |
| Synopsis          | string  | Description as found in the platform.                                                                                                                                   | Guerra…                             |
| Image             | array   | Image URLs that point to the image assets found in the platform belonging to the episode. Not classified. They can be posters, stills or promotional pictures.          | <image src="https://m.media-amazon.com/images/S/pv-target-images//dc7fe3dffbab7f6ca00974653faaf03dadf31b57fdaf47950388a053b4e3547b.jpg" height=100/> |
| Rating            | string  | Age rating information as found in the platform.                                                                                                                        | 16+                                 |
| Provider          | array   | Producer companies, if indicated by the platform.                                                                                                                       | ["Amazon Studios"]                  |
| Genres            | array   | Genres in English, parsed from the genres provided by the platform.                                                                                                     | ["Action","Adventure","Drama","Science Fiction"] |
| GenresPlatform    | array   | Genres as shown by the platform.                                                                                                                                        | ["Acción","Aventura","Drama","Ciencia ficción"] |
| Cast              | array   | Cast members listed by the platform.                                                                                                                                    | ["Sarita Choudhury","Rebecca Watson","Michael Mulheren",...] |
| Directors         | array   | Directors of the episode as listed by the platform.                                                                                                                     | ["Wayne Yip"]                       |
| Download          | boolean | Indicates whether the content can be downloaded for offline watching.                                                                                                   | `false`, `true`, `null`             |
| IsAdult           | boolean | Whether the content is for adult audiences only (erotic, pornographic). Only if specified by the platform.                                                              | `false`, `true`, `null`             |
| UserData          | array   | List of attributes and values related to platform users, such as likes.                                                                                                 | [view in UserData](#userdata)       |
| Packages          | array   | Business models available for the episode.                                                                                                                              | [view in Packages](#packages)       |
| CreatedAt         | string  | Date and time of the episode creation.                                                                                                                                  | 2024-04-20T00:00:00Z                |

#### OtherIds
| Field | Type   | Description                                        | Example                          |
|-------|--------|----------------------------------------------------|----------------------------------|
| Id    | string | Unique identifier for the movie or series.         | 5accc281a08231033065169891875820 |
| Name  | string | Name associated with the identifier (optional).    | CompactGTI                       |

#### ExternalIds
| Field       | Type   | Description                                                      | Example             |
|-------------|--------|------------------------------------------------------------------|---------------------|
| Provider    | string | External database provider (imdb, tmdb, tvdb, eidr).             | imdb                |
| ID          | string | Identifier from the external database.                           | tt10954600          |
| ContentType | string | Type defined in the external database (Tv Show, Episode, Movie). | Movie               |

#### Deeplinks
| Field   | Type   | Description                              | Example                                         |
|---------|--------|------------------------------------------|-------------------------------------------------|
| Web     | string | URL for web platforms.                   | https://www.disneyplus.com/movies/ant-man-and-the-wasp-quantumania/7OLRMMgd1vkx |
| Android | string | URL for Android platforms (optional).    | disneyplus://disneyplus.com/video/498649d2-a45d-4d77-910c-f5fe1e837a90 |
| iOS     | string | URL for iOS platforms (optional).        | disneyplus://disneyplus.com/video/498649d2-a45d-4d77-910c-f5fe1e837a90 |

#### Crew
| Field | Type   | Description                              | Example                       |
|-------|--------|------------------------------------------|-------------------------------|
| Role  | string | Role of the crew member on the platform. | Producer                      |
| Name  | string | Name of the crew member.                 | Kevin Feige                   |

#### Packages
| Field           | Type   | Description                                                                                         | Example                       |
|-----------------|--------|-----------------------------------------------------------------------------------------------------|-------------------------------|
| Type            | string | Type of business model (transaction-vod, subscription-vod, validated-vod, tv-everywhere, free-vod). | transaction-vod               |
| Definition      | string | Video resolution for the package (optional, HD, SD, 4K, 8K).                                        | HD                            |
| BuyPrice        | number | Price for purchasing the content (optional).                                                        | 9.99                          |
| RentPrice       | number | Price for renting the content (optional).                                                           | 3.99                          |
| Currency        | string | Currency code (optional, ISO 4217).                                                                 | USD                           |
| License         | array  | License types (optional, VOD, EST).                                                                 | VOD                           |
| Plan            | string | Special subscription including this content,  such as an Amazon channel (optional).                 | HBO Max                       |
| SeasonRentPrice | number | Price for renting the season (optional) `Only Episodes`.                                            | 10.00                         |
| SeasonBuyPrice  | number | Price for purchasing the season (optional) `Only Episodes`.                                         | 25.00                         |

#### Seasons
| Field     | Type   | Description                                              | Example                         |
|-----------|--------|----------------------------------------------------------|---------------------------------|
| Number    | integer| Season number (optional).                                | 3                               |
| Episodes  | integer| Number of episodes available for that season (optional). | 10                              |
| Year      | integer| Year of release for the season (optional).               | 2009                            |
| SeasonId  | string | Season ID used by the platform (optional).               | 70155472                        |
| Title     | string | Title of the season.                                     | Season 3                        |
| Deeplink  | string | Deeplink for the season (optional).                      | https://www.netflix.com/us/title/70136153 |
| OtherIds  | array  | Other identifiers for the season.                        | [view in OtherIds](#otherids)   |
| Packages  | array  | Business models available within the season.             | `[{"Type": "subscription-vod","Episodes": 10}]` |

#### PopularityRankingBy
| Field | Type    | Description                                        | Example                       |
|-------|---------|----------------------------------------------------|-------------------------------|
| Top   | string  | Name of the ranking as it appears on the platform. | TelecineDaSemana              |
| Value | integer | Rank assigned to the content on the platform.      | 1                             |

#### UserData
| Field | Type     | Description                                        | Example                       |
|-------|----------|----------------------------------------------------|-------------------------------|
| Name  | string   | Name of the attribute. (Favorites, Likes)          | Favorites                     |
| Value | integer  | Value of the attribute at the time of survey.      | 2000                          |

### Stats
| Field           | Type    | Description                                                                                                                             | Example                |
|-----------------|---------|-----------------------------------------------------------------------------------------------------------------------------------------|------------------------|
| PlatformId      | integer | ID for the platform. The ID refers to the platform across all available territories.                                                    | 266                    |
| PlatformCode    | string  | Code identifying the platform and the territory.                                                                                        | us.disneyplus          |
| PlatformName    | string  | Official name of the platform.                                                                                                          | Disney+                |
| PlatformCountry | string  | Country ISO 3166-1 alpha-2 code.                                                                                                        | US                     |
| NullRate        | array   | Shows the rate of null values in each mandatory variable across the whole dataset of the platform in that day, grouped by content type. | `Array <Dict>`         |
| LastUpdates     | string  | Date and time of the last updates.                                                                                                      | 2017-07-21T17:32:28Z   |
| Total           | array   | Total count of each available content type.                                                                                             | `Array <Dict>`         |
| Match           | array   | Match rate grouped by provider (external database).                                                                                     | `Array <Dict>`         |
| CreatedAt       | string  | Date and time of creation.                                                                                                              | 2017-07-21T17:32:28Z   |

## Table Visualization & Data Relationships
We include tables to clearly visualize the relationships and key fields in each JSONL file and analyze how the various files interrelate to provide a complete view of the overall Streaming Availability product data model.

![Streaming Availability](https://github.com/BB-Media-IT/Data-Hub/assets/4085605/85d6bf4e-e051-45fb-8cd5-005e8f90f9f9)

>👋 For more information and pricing details, please feel free to [click here](mailto:hello@bb-media.com?subject=Let's%20Unlock%20Amazing%20Deals%20Together!)! We'd love to help you.
