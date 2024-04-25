# Livestreaming & Fast Channels

This document details the schemas used to manage the data for the `Livestreaming & Fast Channels` product. During the delivery process, a specific S3 Bucket is generated for each client. In each of these buckets, we have three main folders that contain 
JSONL format files. These folders are organized as follows: `channels`, `contents`, `schedule` and `sports`. Additionally, within each of these main folders, there is a subfolder called `latest`, where the latest snapshot from each streaming platform surveyed and 
contracted by the client is stored.

## Document Structure
This document is organized into the following sections:

- [**File Description**](#file-description)
- [**Table Visualization & Data Relationships**](#table-visualization--data-relationships)

## Details of the S3 Buckets
Each client receives an S3 Bucket where data is organized into specific folders to ensure efficient management and quick access. The folder names reflect the types of data they contain, facilitating the identification and specific processing of each data set:

#### Example: 
- `s3://bucket-client/LiveStreaming/channels`
- `s3://bucket-client/LiveStreaming/contents`
- `s3://bucket-client/LiveStreaming/schedule`
- `s3://bucket-client/LiveStreaming/sports`

This folder contains a `latest` subfolder, which is periodically updated with the latest available snapshot, ensuring that customers always have access to the latest information.

#### Update frequency and scope
- The update of the data in S3 Bucket is defined according to the needs of each customer.
- The scope is defined according to the needs of each customer.

🚀 You can get a weekly updated demo by connecting to the following Bucket `s3://bb-media-data/live-streaming/` using AWS CLI or any software and the endpoint parameter `--endpoint https://nyc3.digitaloceanspaces.com`.

>**Command example** `aws s3 --endpoint https://nyc3.digitaloceanspaces.com cp s3://bb-media-data/live-streaming/ /Demo/BB-Media --recursive`

## File Description
We provide a detailed description of the files contained in the `Sources` folder, explaining the structure and type of data handled by each one. If you wish to see the schemas in YAML, [click here](schemas-yml).

### chanles
| Field | Type | Description | Example |
|-------|------|-------------|---------|
| PlatformNumberId | integer | ID for the platform. The ID refers to the platform across all available territories. | 755 |
| PlatformCountry | string | Country ISO 3166-1 alpha-2 code. | US |
| PlatformCode | string | Code identifying the platform and the territory. | us.plutotv |
| CreatedAt | string | Date when the data was scraped. | 2023-09-24 |
| Timestamp | date | Timestamp when the scraping started. | 2023-09-24T15:27:37.238000 |
| Id | string | Channel ID either brought from the platform or hashed. | 569546031a619b8f07ce6e25 |
| Title | string | Channel title. | Pluto TV Horror |
| Type | string | Channel type. Value assigned to the channel (not scraped). | TV |
| Deeplink | string | Channel deeplink. | https://pluto.tv/es/live-tv/pluto-tv-horror |
| Broadcast | string | MRL link if found. | https://example.com/live/index.m3u8 |
| Number | integer | Channel number if found. | 96 |
| Images | array | Channel images. | [View More In Images](#images) |
| Genres | array | Channel genres. | ["News","Sports"] |
| Subtitles | array | Subtitles available. | ["English","Spanish"] |
| Dubbed | array | Spoken languages available. | ["English","Spanish"] |
| FullDay | boolean | Channel has no schedule defined but has 24 hours transmission. | `false` `true` |
| IsOriginal | boolean | Platform original content. | `false` `true` |
| IsAdult | boolean | Adult content or with age restriction. | `false` `true` |
| IsKids | boolean | Kids content. | `false` `true` |
| IsFast | boolean | Provides FAST content. Value assigned to the channel (not scraped). | `false` `true` |
| FastBy | string | FAST type. Value assigned to the channel (not scraped). | `By Content` |
| Owner | string | Channel owner. Value assigned to the channel (not scraped). | `Paramount Global` |
| Packages | array | Channel revenue model. | [View More In Packages](#packages) |
| GMT | integer | GMT timezone offset. | -4 |
| IsActive | boolean | Indicates whether the channel was found active during the scraping. | `false` `true` |

#### Images
| Field | Type | Description | Example |
|-------|------|-------------|---------|
| Type | string | Image type. | `Logo` |
| Url | string | Direct URL for the image. | <img src="https://images.pluto.tv/channels/569546031a619b8f07ce6e25/logo.png?fit=fill&fm=png&h=80&w=280" height=60> |

#### Packages
| Field | Type | Description | Example |
|-------|------|-------------|---------|
| Type | string | Type of business model (transaction-vod, subscription-vod, validated-vod, tv-everywhere, free-vod). | free-vod |

### contents
| Field | Type | Description | Example |
|-------|------|-------------|---------|
| PlatformNumberId | integer | ID for the platform. The ID refers to the platform across all available territories.  | 755 |
| PlatformCountry | string | Country ISO 3166-1 alpha-2 code. | US |
| PlatformCode | string | Code identifying the platform and the territory. | us.plutotv |
| CreatedAt | string | Date when the data was scraped. | 2023-08-28 |
| Timestamp | date | Timestamp when the scraping started. | 2023-08-28T04:19:39.052000 |
| Id | string | Unique identifier for the content. | 58c058af77914d67bfdbdec9 |
| Title | string | Title of the content. | Texas Chainsaw |
| Type | string | Type of the content. undefined: Type cannot be determined. placeholder: No content data available.  One of: movie, episode, undefined, placeholder | movie |
| Deeplink | string | Deeplink for the content. | https://pluto.tv/es/live-tv/pluto-tv-terror/details/texas-chainsaw-massacre-3d-1-1 |
| Year | integer | Year of the content. | 1970 |
| Synopsis | string | Synopsis of the content. | A young woman inherits an isolated mansion... |
| Images | array | Images associated with the content. | <img src="https://images.pluto.tv/episodes/58c058af77914d67bfdbdec9/poster.jpg?fill=blur&fit=fill&fm=jpg&h=1000&q=75&w=694" height=200> |
| Duration | integer | Duration of the content in minutes. | 120 |
| Genres | array | Genres associated with the content. | ["Horror"] |
| Rating | string | Content rating. | R |
| OnDemand | boolean | Whether the content is available on-demand. | `false` `true` `null` |
| IsAdult | boolean | Whether the content is adult-oriented. | `false` `true` `null` |
| IsKids | boolean | Whether the content is kids-oriented. | `false` `true` `null` |
| SerieTitle | string | Title of the series if the content is part of a series. | `null` |
| Season | integer | Season number if the content is part of a series. | `null` |
| Episode | integer | Episode number if the content is part of a series. | `null` |
| Packages | array | Revenue models assiciated with the content. | [View More In Packages](#packages) |

### schedule
| Field | Type | Description | Example |
|-------|------|-------------|---------|
| PlatformNumberId | integer | ID for the platform. The ID refers to the platform across all available territories. | 755 |
| PlatformCountry | string | Country ISO 3166-1 alpha-2 code. | US |
| PlatformCode | string | Code identifying the platform and the territory. | us.plutotv |
| CreatedAt | string | Date when the data was scraped. | 2024-04-13 |
| Timestamp | date | Timestamp when the scraping started. | 2024-04-13T08:18:00.484000 |
| Id | string | Unique identifier for the payload schedule. | a84aeb8ff4e696fbfab88756e7fbf6ec |
| ChannelId | string | Unique identifier for the channel associated with the payload. | 5dc481cda1d430000948a1b4 |
| ChannelTitle | string | Title of the channel. | CBS News Los Angeles |
| ContentId | string | Unique identifier for the content associated with the payload. | 63b67c9bbc65210013550c75 |
| ContentTitle | string | Title of Content | KCAL News 5pm |
| Type | string | Type of the payload. placeholder: No schedule data available. | schedule |
| Subtitles | array | Subtitles available for the content. | ["English","Spanish"] |
| Dubbed | array | Spoken languages available for the content. | ["English","Spanish"] |
| ClosedCaption | boolean | Whether closed captions are available. | `false` `true` `null` |
| Accessibility | boolean | Has accesibility options. | `false` `true` `null` |
| IsFast | boolean | Whether the schedule's channel is FAST. Value assigned to the channel (not scraped). | `false` `true` `null` |
| StartDate | date | Start time of the payload schedule. | 2024-04-13T20:00:00 |
| EndDate | date | End time of the payload schedule. | 2024-04-13T21:00:00 |
| Duration | integer | Duration of the content in minutes. | 60 |
| Seconds | integer | Duration of the content in seconds. | 3600 |
| GMT | integer | GMT timezone offset. | -4 |

### sports
We are moving forward in our live sporting events project. We are currently adapting our schemas to align with [schema.org](https://schema.org) standards, ensuring easy integration for clients. Focusing on major sports and leagues, we plan to release the initial version of the schema in `May 2024`. We will make every effort to ensure that this version will also include additional data, such as lineups and detailed information about teams and players.

| Field                 | Type     | Description | Example |
|-----------------------|----------|-------------|---------|
| `@context`            | String   | The schema that defines the data context, typically a URL pointing to a definition like Schema.org. | http://schema.org |
| `@type`               | String   | The type of this entity, here it is a `BroadcastEvent`. | BroadcastEvent |
| `event_id`            | String   | Unique event HashId |5e54254cbc74b8562a16619622d3be41333383e128d72c7a24dab9e9a3e57db0 |
| `isLiveBroadcast`     | Boolean  | Indicates if the event is a live broadcast. | `false` `true` |
| `eventAttendanceMode` | String   | Mode of attendance, here specified as `OnlineEventAttendanceMode` indicating an online event. | OnlineEventAttendanceMode |
| `broadcastOfEvent`    | Object   | An embedded object that describes the sports event being broadcast. Details follow in nested dictionary. | [View More In broadcastOfEvent](#nested-within-broadcastofevent) |

#### Nested within broadcastOfEvent
| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `@type` | String | Specifies the type | SportsEvent |
| `sport` | String | The type of sport. | Baseball |
| `organizer` | Object | Object detailing the organizer. | [View More In organizer](#nested-within-organizer) |
| `eventStatus` | String | The status of the event. | EventScheduled |
| `name` | String | Name of the sports event, same as the broadcast event. | Seattle Mariners vs. Texas Rangers |
| `description` | String | Description of the sports event, same as the broadcast event. | Seattle Mariners vs. Texas Rangers MLB 2024 |
| `awayTeam` | Object | Details about the away team, specified further in nested dictionary. | [View More In awayTeam](#nested-within-awayteam-and-hometeam) |
| `homeTeam` | Object | Details about the home team, specified further in nested dictionary. | [View More In awayTeam](#nested-within-awayteam-and-hometeam) |
| `startDate` | DateTime | Start date and time for the sports event, matches the broadcast event. | 2024-04-24T00:05:00Z |
| `location` | Object | The location of the event, described further in nested dictionary. | [View More In location](#nested-within-location) |
| `offers` | Object | Offers related to the event, including pricing and URLs, described further in nested dictionary. | [View More In offers](#nested-within-offers) |
| `audience` | Object | The intended audience for the event. | Sports Fans |

#### Nested within organizer
| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `@type` | String | Type of the entity | Organization |
| `name` | String | Name of the Organizer | MLB |
| `logo` | String | Logo of the Organizer | <img src="https://dlv.nyc3.cdn.digitaloceanspaces.com/sports/events/bb_logo_mlb.png" height=80>

#### Nested within `awayTeam` and `homeTeam`
| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `@type` | String | Type of the entity | SportsTeam |
| `name` | String | Name of the team or player | Seattle Mariners |
| `sport` | String | Sport played by the team | Baseball |
| `logo` | String | Logo the team or player | <img src="https://dlv.nyc3.cdn.digitaloceanspaces.com/sports/teams/mlb_seattle_mariners.png" height=80/> |

#### Nested within `location`
| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `@type` | String | Type. | SportsActivityLocation |
| `name` | String | The name of the location | Globe Life Field |

#### Nested within `offers`
| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `@type` | String | Type. | AggregateOffer |
| `highPrice` | Number | The highest price of the offers, if available. | `null` |
| `lowPrice` | Number | The lowest price of the offers, if available. | `null` |
| `offerCount` | Number | The count of distinct offers available. | 2 |
| `offers` | Array | Array of individual offers, each described further. | [View More In offers](#nested-within-individual-offers-in-offers) |

#### Nested within individual `offers` in `offers`
| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `@type` | String | Type. | Offer |
| `name` | String | Name of the offer. | Amazon Prime Video |
| `url` | URL as string | URL where the offer can be accessed. | https://watch.amazon.com/detail?gti=amzn1.dv.gti.01ab1375-a637-4662-a3b9-84940f16764f |

## Table Visualization & Data Relationships
We include tables to clearly visualize the relationships and key fields in each JSONL file and analyze how the various files interrelate to provide a complete view of the overall `Livestreaming & Fast Channels` product data model.

![Livestreaming](https://github.com/BB-Media-IT/Data-Hub/assets/4085605/c903e760-8a4a-4881-8f51-8d9c033fc1aa)

>👋 For more information and pricing details, please feel free to [click here](mailto:hello@bb-media.com?subject=Let's%20Unlock%20Amazing%20Deals%20Together!)! We'd love to help you.
