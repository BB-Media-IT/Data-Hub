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
We provide a detailed description of the files contained in the `Contents`, `Episodes`, and `Stats` folders, explaining the structure and type of data each one manages.

### Contents
| Field                 | Type     | Description                                                                                                  | Example                            |
|-----------------------|----------|--------------------------------------------------------------------------------------------------------------|------------------------------------|
| PlatformId            | integer  | ID for the platform.                                                                                         | 651                                |
| PlatformCode          | string   | Code identifying the platform and the territory.                                                             | us.netflix                         |
| PlatformName          | string   | Official name of the platform.                                                                               | Netflix                            |
| PlatformCountry       | string   | Country ISO 3166-1 alpha-2 code.                                                                             | US                                 |
| HashUnique            | string   | Hash identifying the movie or series in a specific platform and territory.                                   | 552c3a2cbde3e57c92d9f0cd9762c096   |
| UID                   | string   | Hash identifying the movie or series universally.                                                            | badaa0209ebde1ea3251196a51885290   |
| Id                    | string   | Identifier of the movie or series used in the platform itself.                                               | 60004473                           |
| OtherIds              | array    | Only for Amazon platforms. The ASIN, GTI and CompactGTI IDs, when available.                                 | [view in OtherIds](#otherids)      |
| Title                 | string   | The title as it is found in the platform.                                                                    | Jurassic Park III [Dub]            |
| CleanTitle            | string   | Title stripped of parentheses and other additions that don't belong to the title.                            | Jurassic Park III                  |
| OriginalTitle         | string   | Title in the original language.                                                                              | Jurassic Park III                  |
| Type                  | string   | The content type as it is assigned by the platform.                                                          | Movie, Tv Show                     |
| Year                  | integer  | The release year as it is listed by the platform.                                                            | 2001                               |
| Duration              | integer  | Runtime in minutes.                                                                                          | 92                                 |
| ExternalIds           | array    | IDs from external databases that are mapped to the UID assigned to the movie or series.                      | [view in ExternalIds](#externalids)|
| Deeplinks             | object   | URLs pointing to the movie or series in the platform.                                                        | [view in Deeplinks](#deeplinks)    |
| PlaybackLink          | string   | URL that will immediately play the content on open.                                                          | https://netflix.com/watch/60004473 |
| Synopsis              | string   | Description as found in the platform.                                                                        | An aerial tour of an infamous...   |
| Image                 | array    | Image URLs that point to the image assets found in the platform belonging to the movie or series.            | <image src="https://occ-0-472-444.1.nflxso.net/dnm/api/v6/E8vDc_W8CLv7-yMQu8KMEC7Rrr8/AAAABZ0BssOES4V8JXr7KwPi-dWUTscZ_E_B5uBCVv1vhovnh4x4v9VBAIBwlRgm6ODkBTA6B69XrmsslxOvN015e9TBVbbvaKSuqooZ.webp?r=70b" height=100/> |
| Rating                | string   | Age rating information as found in the platform.                                                             | PG-13                              |
| Provider              | array    | Producer companies, if indicated by the platform.                                                            | ["PARAMOUNT"]                      |
| Genres                | array    | Genres in English, parsed from the genres provided by the platform.                                          | ["Comedy"]                         |
| GenresPlatform        | array    | Genres as shown by the platform.                                                                             | ["Films Based on Books","Action & Adventure Films"] |
| Cast                  | array    | List of names from the cast, as provided by the platform.                                                    | ["Arnold Schwarzenegger","Grace Jones"] |
| Crew                  | array    | List of crew members and their roles.                                                                        | [view in Crew](#crew)              |
| Directors             | array    | In the case of series, it may contain the series creators or episode directors.                              | ["Richard Fleischer"]              |
| Download              | boolean  | Indicates whether the content can be downloaded for offline watching.                                        | true, false                        |
| IsOriginal            | boolean  | Whether the content is original to the platform.                                                             | true, false                        |
| IsAdult               | boolean  | Whether the content is for adult audiences only.                                                             | true, false                        |
| Packages              | array    | Business models available for the movie or series.                                                           | [view in Packages](#packages)      |
| CreatedAt             | string   | Indicates the time the data was scraped from the platform.                                                   | 2017-07-21T17:32:28Z               |
| IsBranded             | boolean  | Whether the content shows the platform branding.                                                             | true, false                        |
| IsExclusive           | boolean  | Whether the content is exclusive to the platform.                                                            | true, false                        |
| IsPremium             | boolean  | Whether the content requires an upgrade over the basic subscription.                                         | true, false                        |
| Seasons               | array    | Information about seasons if applicable.                                                                     | [view in Seasons](#seasons)        |
| Subtitles             | array    | List of available subtitle languages as ISO 639-2 codes.                                                     | ["en","es","pt"]                   |
| Dubbed                | array    | List of available dub languages as ISO 639-2 codes.                                                          | ["en","es","pt"]                   |
| PopularityRankingBy   | array    | List of platform rankings and corresponding rank for the content.                                            | [view in PopularityRankingBy](#popularityrankingby)|
| UserData              | array    | List of attributes and values related to platform users, such as likes.                                      | [view in Packages](#packages)      |

#### OtherIds
| Field | Type   | Description                                        | Example                          |
|-------|--------|----------------------------------------------------|----------------------------------|
| Id    | string | Unique identifier for the movie or series.         | 5accc281a08231033065169891875820 |
| Name  | string | Name associated with the identifier (optional).    | CompactGTI                       |

#### ExternalIds
| Field       | Type   | Description                                                      | Example             |
|-------------|--------|------------------------------------------------------------------|---------------------|
| Provider    | string | External database provider (imdb, tmdb, tvdb, eidr).             | imdb                |
| ID          | string | Identifier from the external database.                           | tt4154796           |
| ContentType | string | Type defined in the external database (Tv Show, Episode, Movie). | Movie               |

#### Deeplinks
| Field   | Type   | Description                              | Example                                         |
|---------|--------|------------------------------------------|-------------------------------------------------|
| Web     | string | URL for web platforms.                   | https://www.netflix.com/us/title/393326         |
| Android | string | URL for Android platforms (optional).    | nflx://netflix.com/watch/393326                 |
| iOS     | string | URL for iOS platforms (optional).        | nflx://netflix.com/watch/393326                 |

### Crew
| Field | Type   | Description                              | Example                       |
|-------|--------|------------------------------------------|-------------------------------|
| Role  | string | Role of the crew member on the platform. | Director                      |
| Name  | string | Name of the crew member.                 | Richard Fleischer             |

#### Packages
| Field      | Type   | Description                                                                                         | Example                       |
|------------|--------|-----------------------------------------------------------------------------------------------------|-------------------------------|
| Type       | string | Type of business model (transaction-vod, subscription-vod, validated-vod, tv-everywhere, free-vod). | transaction-vod               |
| Definition | string | Video resolution for the package (optional, HD, SD, 4K, 8K).                                        | HD                            |
| BuyPrice   | number | Price for purchasing the content (optional).                                                        | 9.99                          |
| RentPrice  | number | Price for renting the content (optional).                                                           | 3.99                          |
| Currency   | string | Currency code (optional, ISO 4217).                                                                 | USD                           |
| License    | array  | License types (optional, VOD, EST).                                                                 | VOD                           |
| Plan       | string | Special subscription including this content (optional).                                             | HBO Max                       |

#### Seasons
| Field     | Type   | Description                                              | Example                         |
|-----------|--------|----------------------------------------------------------|---------------------------------|
| Number    | integer| Season number (optional).                                | 1                               |
| Episodes  | integer| Number of episodes available for that season (optional). | 10                              |
| Year      | integer| Year of release for the season (optional).               | 2019                            |
| SeasonId  | string | Season ID used by the platform (optional).               | s01                             |
| Title     | string | Title of the season.                                     | Season 1                        |
| Deeplink  | string | Deeplink for the season (optional).                      | https://www.example.com/season1 |
| OtherIds  | array  | Other identifiers for the season.                        |                                 |
| Packages  | array  | Business models available within the season.             |                                 |

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

## Table Visualization & Data Relationships
We include tables to clearly visualize the relationships and key fields in each JSONL file and analyze how the various files interrelate to provide a complete view of the overall Streaming Availability product data model.



---------------------------

👋 For more information and pricing details, please feel free to [click here](mailto:hello@bb-media.com?subject=Let's%20Unlock%20Amazing%20Deals%20Together!)! We'd love to help you.