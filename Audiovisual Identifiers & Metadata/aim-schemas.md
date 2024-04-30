# Audiovisual Identifiers & Metadata

This document details the schemas used to manage the `Audiovisual Identifiers & Metadata` product data. During the delivery process, a specific S3 Bucket is created for each client. In each of these buckets, we have a main folder containing files in JSONL format. This folder is named `Sources`. Additionally, within this folder, there is a subfolder named `latest`, where the latest snapshot of the `Metadata BB` database is stored.

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
- The scope is defined according to the needs of each customer, guaranteeing at least `Metadata BB`.

🚀 You can get a weekly updated demo by connecting to the following Bucket `s3://bb-media-data/audiovisual-identifier-and-metadata/` using AWS CLI or any software and the endpoint parameter `--endpoint https://nyc3.digitaloceanspaces.com`.

>**Command example** `aws s3 --endpoint https://nyc3.digitaloceanspaces.com cp s3://bb-media-data/audiovisual-identifier-and-metadata/ /Demo/BB-Media --recursive`

## File Description
We provide a detailed description of the files contained in the `Sources` folder, explaining the structure and type of data handled by each one. If you wish to see the schemas in YAML, [click here](schemas-yml).

### BBIDs
| Field        | Type   | Description                                                               | Example                          |
|--------------|--------|---------------------------------------------------------------------------|----------------------------------|
| UID          | string | The ID created by BB which identifies a group of external IDs.            | f6343770f9212ebc396d74d21354ad33 |
| ExternalIds  | array  | -                                                                         | [View More In ExternalIds](#externalids) |

#### ExternalIds
| Field      | Type   | Description                                                   | Example                            |
|------------|--------|---------------------------------------------------------------|------------------------------------|
| UID        | string | The ID created by BB which identifies a group of external IDs.| f6343770f9212ebc396d74d21354ad33   |
| Provider   | string | Identifies the source of the ID.                              | eidr                               |
| ID         | string | The ID from the external provider.                            | 10.5240/8805-D5B9-3435-1B99-E538-L |
| Type       | string | The type assigned by the external provider.                   | Movie                              |
| CreatedAt  | string | The time when the ID was inserted in our database.            | 2023-04-10T20:39:33Z               |
| UpdatedAt  | string | The time when the ID was last updated in our database.        | 2024-04-21T04:59:04Z               |

### SourcesContents
| Field         | Type    | Description                                     | Example     |
|---------------|---------|-------------------------------------------------|-------------|
| UID           | string  | Universal BB ID.                                | f6343770f9212ebc396d74d21354ad33 |
| Source        | string  | Source of the metadata.                         | bb          |
| Id            | string  | ID in the external database.                    | `null`      |
| Title         | string  | Content title.                                  | Star Wars: The Rise of Skywalker |
| OriginalTitle | string  | Title in the original language.                 | Star Wars: The Rise of Skywalker |
| Year          | integer | Year of release.                                | 2019        |
| Directors     | array   | List of directors.                              | ["J.J. Abrams"] |
| CreatedBy     | array   | Name of the creator.                            | `null`      |
| Cast          | array   | List of cast.                                   | ["Carrie Fisher","Mark Hamill","Daisy Ridley",...] |
| Crew          | array   | List of crew who worked in the title.           | [View More In Crew](#crew) |
| Akas          | array   | List of localized titles for different regions. | [View More In Akas](#akas) |
| Country       | array   | List of production countries.                   | ["US"]      |
| Companies     | array   | List of companies involved in the production and distribution of this title. | [View More In Companies](#companies) |
| Synopsis      | array   | List of synopsis and their languages            | [View More In Synopsis](#synopsis) |
| Images        | array   | URLs to different kinds of images.              | [View More In Images](#images) |
| Videos        | array   | Trailers or other promotional videos.           | [View More In Videos](#videos) |
| Languages     | array   | Languages used in the title.                    | ["en"]      |
| ReleaseYears  | array   | List of release years by territory.             | [View More In ReleaseYears](#releaseyears) |
| ReleaseDate   | string  | Global release day                              | 2019-12-18  |
| Duration      | integer | Runtime in minutes.                             | 142         |
| Genres        | array   | List of genres                                  | ["Adventure","Action","Science Fiction"] |
| Homepage      | string  | Website for the content.                        | https://www.starwars.com/films/star-wars-episode-ix-the-rise-of-skywalker |
| Keywords      | array   | List of keywords                                | ["Space"]   |
| Status        | string  | Content status.                                 | `null` `Planned` `Pilot` `In Production` `Returning` `Canceled` `Ended` |
| Type          | string  | Content type.                                   | Movie       |
| IsAdult       | boolean | Flag indicating whether the title is for adult audiences. | `true` `false` |
| Franchise     | string  | Name of the franchise the title belongs to.     | `null`         |
| Scripted      | boolean | -                                               | `true` `false` |
| Seasons       | array   | -                                               | [View More In Seasons](#seasons) |
| Rating        | array   | Age rating.                                     | PG-13          |
| CreatedAt     | string  | Indicates when the record was created.          | 2023-04-10T20:39:33Z |
| UpdatedAt     | string  | Indicates when the record was updated.          | 2024-04-21T04:59:04Z |


#### Crew
| Field | Type   | Description | Example         |
|-------|--------|-------------|-----------------|
| Name  | string | -           | Michelle Rejwan |
| Role  | string | -           | Producer        |

#### Akas
| Field    | Type   | Description | Example    |
|----------|--------|-------------|------------|
| Language | string | ISOAlpha2   | kr         |
| Region   | string | ISOAlpha2   | KR         |
| Title    | string | -           | 스타워즈-라이즈 오브 스카이워커 |

#### Companies
| Field   | Type   | Description | Example |
|---------|--------|-------------|---------|
| Country | string | ISOAlpha2   | US      |
| Name    | string | -           | Lucasfilm Ltd. |
| Type    | string | Production or distributor company.       | Production |

#### Synopsis
| Field       | Type   | Description | Example |
|-------------|--------|-------------|---------|
| Region      | string | ISOAlpha2   | JP      |
| Language    | string | ISOAlpha2   | ja      |
| Description | string | -           | かつて銀河に君臨していた祖父ダース・ベイダーに傾倒し... |

#### Images
| Field    | Type   | Description | Example |
|----------|--------|-------------|---------|
| Type     | string | -           | `Poster` `Backdrop` `Thumbnail` `Logo` `null` |
| Language | string | ISOAlpha2   | `null`  |
| URL      | string | Original URL.         | `null`  |
| BBURL    | string | Image URL hosted by BB.          | <img src="https://dlv.nyc3.digitaloceanspaces.com/images/db32LaOibwEliAmSL2jjDF6oDdj-154.jpg"/> |

#### Videos
| Field    | Type   | Description | Example     |
|----------|--------|-------------|-------------|
| Provider | string | -           | YouTube     |
| Id       | string | -           | oln5JMXRT9U |
| Language | string | ISOAlpha2   | en          |
| Type     | string | -           | Featurette  |

#### ReleaseYears
| Field   | Type    | Description | Example |
|---------|---------|-------------|---------|
| Country | string  | ISOAlpha2   | US      |
| Year    | integer | -           | 2019    |

#### Seasons
| Field    | Type    | Description          | Example   |
|----------|---------|----------------------|-----------|
| Number   | integer | Season number.       | 1         |
| Episodes | integer | Number of episodes.  | 10        |
| Year     | integer | N/D                  | 2023      |
| SeasonId | integer | N/D                  | 333987    |
| Title    | string  | N/D                  | Seasons 1 |

### SourcesImages
| Field      | Type   | Description                                            | Example                          |
|------------|--------|--------------------------------------------------------|----------------------------------|
| UID        | string | Content ID by BB.                                      | f6343770f9212ebc396d74d21354ad33 |
| ID         | string | Content ID determined by the provider.                 | 181812                           |
| Type       | string | Content type determined by the provider.               | Movie                            |
| Provider   | string | Identifies where the images were sourced.              | tmbd                             |
| Images     | array  | -                                                      | [View More In Images](#s-images) |
| Seasons    | array  | -                                                      | [View More In Seasons](#s-seasons) |
| CreatedAt  | string | Indicates when the record was created in our database. | 2024-04-21T04:03:02Z             |

#### S-Images
| Field    | Type   | Description | Example                                       |
|----------|--------|-------------|-----------------------------------------------|
| Type     | string | -           | `Poster` `Backdrop` `Thumbnail` `Logo` `null` |
| ImageUrl | string | -           | <img src="https://dlv.nyc3.digitaloceanspaces.com/images/jOzrELAzFxtMx2I4uDGHOotdfsS-154.jpg"> |

#### S-Seasons
| Field    | Type   | Description   | Example                                         |
|----------|--------|---------------|-------------------------------------------------|
| ID       | string | -             | 125919                                          |
| Number   | integer| Season number.| 1                                               |
| Images   | array  | -             | [View More In Season Images](#season-images)    |
| Episodes | array  | -             | [View More In Episodes](#episodes)              |

#### Season Images
| Field    | Type   | Description | Example                                       |
|----------|--------|-------------|-----------------------------------------------|
| Type     | string | -           | `Poster` `Backdrop` `Thumbnail` `Logo` `null` |
| ImageUrl | string | -           | <img src="https://dlv.nyc3.digitaloceanspaces.com/images/ozHgksxrAu3uzi7axD1XavC58To-154.jpg" /> |

#### Episodes
| Field    | Type   | Description    | Example                                       |
|----------|--------|----------------|-----------------------------------------------|
| ID       | integer| -              | 1818809                                       |
| Number   | integer| Episode number.| 1                                             |
| Images   | array  | -              | [View More In Episode Images](#episode-images)|

#### Episode Images
| Field    | Type   | Description | Example        |
|----------|--------|-------------|----------------|
| Type     | string | -           | `Still`        |
| ImageUrl | string | -           | <img src="https://dlv.nyc3.digitaloceanspaces.com/images/fe8vz1SEVQkwOe4XBUcFNrg6oxu-154.jpg" /> |

### SourcesPopularity
| Field           | Type    | Description                                            | Example                  |
|-----------------|---------|--------------------------------------------------------|--------------------------|
| UID             | string  | Hash identifying the movie or series universally.      | f6343770f9212ebc396d74d21354ad33 |
| Provider        | string  | Identifies the source of the ID.                       | tmdb                     |
| ID              | string  | The ID from the external provider.                     | 181812                   |
| Popularity      | integer | Popularity score in the external provider.             | 68.87                    |
| MetacriticScore | integer | Metacritic score as shown in the external provider.    | `null`                   |
| CreatedAt       | string  | Indicates when the record was created in our database. | 2024-04-21T00:00:00Z     |

### SourcesRatings
| Field     | Type    | Description                                            | Example                  |
|-----------|---------|--------------------------------------------------------|--------------------------|
| UID       | string  | Hash identifying the movie or series universally.      | f6343770f9212ebc396d74d21354ad33 |
| Provider  | string  | Identifies the source of the ID.                       | imdb                     |
| ID        | string  | The ID from the external provider.                     | tt2527338                |
| Votes     | integer | Amount of votes in the external provider.              | 492415                   |
| Score     | number  | Average score in the external provider.                | 6.4                      |
| CreatedAt | string  | Indicates when the record was created in our database. | 2024-04-21T00:00:00Z     |

## Table Visualization & Data Relationships
We include tables to clearly visualize the relationships and key fields in each JSONL file and analyze how the various files interrelate to provide a complete view of the overall `Audiovisual Identifiers & Metadata` product data model.

You can obtain the relationships between all BB Media products in this [link](/File%20Relationships/relationships.md).

![Audiovisual Identifier   Metadata (1)](https://github.com/BB-Media-IT/Data-Hub/assets/4085605/e26de2c4-e3cf-458d-b030-55b4d5fdf2e7)


>👋 For more information and pricing details, please feel free to [click here](mailto:hello@bb-media.com?subject=Let's%20Unlock%20Amazing%20Deals%20Together!)! We'd love to help you.
