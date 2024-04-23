# Streaming Availability
Discover a comprehensive database of movies, series, and episodes available on-demand (OD) in more than 200 regions. Our offering includes a detailed breakdown of business models such as SVOD, AVOD, TVOD, and TVE. ['Content Pulse'](https://bb-media.com/streaming/) provides normalized metadata, while 'Streaming Availability' offers raw data, showcasing how each service communicates its content with universal IDs and enriched with BB Media’s intelligent metadata.

👋 For more information and pricing details, please feel free to [click here](mailto:hello@bb-media.com?subject=Let's%20Unlock%20Amazing%20Deals%20Together!)! We'd love to help you.

## Schema
| Field                 | Type     | Description                                                                                                 | Example                  |
|-----------------------|----------|-------------------------------------------------------------------------------------------------------------|--------------------------|
| PlatformId            | integer  | ID for the platform.                                                                                        |                          |
| PlatformCode          | string   | Code identifying the platform and the territory.                                                           | us.netflix               |
| PlatformName          | string   | Official name of the platform.                                                                              |                          |
| PlatformCountry       | string   | Country ISO 3166-1 alpha-2 code.                                                                            | IE                       |
| HashUnique            | string   | Hash identifying the movie or series in a specific platform and territory.                                  | 5accc281a08231033065169891875820 |
| UID                   | string   | Hash identifying the movie or series universally.                                                           | 3037d326dcfb6bf35f72b09edfb5b114 |
| Id                    | string   | Identifier of the movie or series used in the platform itself.                                              |                          |
| OtherIds              | array    | Only for Amazon platforms. The ASIN, GTI and CompactGTI IDs, when available.                                 |                          |
| Title                 | string   | The title as it is found in the platform.                                                                   |                          |
| CleanTitle            | string   | Title stripped of parentheses and other additions that don't belong to the title.                            |                          |
| OriginalTitle         | string   | Title in the original language.                                                                             |                          |
| Type                  | string   | The content type as it is assigned by the platform.                                                         | Movie, Tv Show           |
| Year                  | integer  | The release year as it is listed by the platform.                                                           |                          |
| Duration              | integer  | Runtime in minutes.                                                                                         |                          |
| ExternalIds           | array    | IDs from external databases that are mapped to the UID assigned to the movie or series.                      |                          |
| Deeplinks             | object   | URLs pointing to the movie or series in the platform.                                                        |                          |
| PlaybackLink          | string   | URL that will immediately play the content on open.                                                          |                          |
| Synopsis              | string   | Description as found in the platform.                                                                       |                          |
| Image                 | array    | Image URLs that point to the image assets found in the platform belonging to the movie or series.           |                          |
| Rating                | string   | Age rating information as found in the platform.                                                             |                          |
| Provider              | array    | Producer companies, if indicated by the platform.                                                            |                          |
| Genres                | array    | Genres in English, parsed from the genres provided by the platform.                                          |                          |
| GenresPlatform        | array    | Genres as shown by the platform.                                                                             |                          |
| Cast                  | array    | List of names from the cast, as provided by the platform.                                                    |                          |
| Crew                  | array    | List of crew members and their roles.                                                                        |                          |
| Directors             | array    | In the case of series, it may contain the series creators or episode directors.                              |                          |
| Download              | boolean  | Indicates whether the content can be downloaded for offline watching.                                        |                          |
| IsOriginal            | boolean  | Whether the content is original to the platform.                                                             |                          |
| IsAdult               | boolean  | Whether the content is for adult audiences only.                                                             |                          |
| Packages              | array    | Business models available for the movie or series.                                                           |                          |
| CreatedAt             | string   | Indicates the time the data was scraped from the platform.                                                    | 2017-07-21T17:32:28Z     |
| IsBranded             | boolean  | Whether the content shows the platform branding.                                                             |                          |
| IsExclusive           | boolean  | Whether the content is exclusive to the platform.                                                            |                          |
| IsPremium             | boolean  | Whether the content requires an upgrade over the basic subscription.                                         |                          |
| Seasons               | array    | Information about seasons if applicable.                                                                     |                          |
| Subtitles             | array    | List of available subtitle languages as ISO 639-2 codes.                                                     |                          |
| Dubbed                | array    | List of available dub languages as ISO 639-2 codes.                                                          |                          |
| PopularityRankingBy   | array    | List of platform rankings and corresponding rank for the content.                                             |                          |
| UserData              | array    | List of attributes and values related to platform users, such as likes.                                      |                          |

### OtherIds:
| Field | Type   | Description                                        | Example                       |
|-------|--------|----------------------------------------------------|-------------------------------|
| Id    | string | Unique identifier for the movie or series.         | 5accc281a08231033065169891875820 |
| Name  | string | Name associated with the identifier (optional).   | Avengers: Endgame           |

### ExternalIds:
| Field       | Type   | Description                                            | Example                       |
|-------------|--------|--------------------------------------------------------|-------------------------------|
| Provider    | string | External database provider (imdb, tmdb, tvdb, eidr).  | imdb                         |
| ID          | string | Identifier from the external database.                | tt4154796                    |
| ContentType | string | Type defined in the external database (Tv Show, Episode, Movie). | Movie                         |

### Deeplinks:
| Field   | Type   | Description                              | Example                       |
|---------|--------|------------------------------------------|-------------------------------|
| Web     | string | URL for web platforms.                   | https://www.example.com/movie |
| Android | string | URL for Android platforms (optional).    | https://www.example.com/movie/android |
| iOS     | string | URL for iOS platforms (optional).        | https://www.example.com/movie/ios |

### Image:
| Field | Type   | Description                                     | Example                       |
|-------|--------|-------------------------------------------------|-------------------------------|
| URL   | string | URL pointing to an image asset of the content. | https://www.example.com/images/movie.jpg |

### Provider:
| Field | Type   | Description                                | Example                       |
|-------|--------|--------------------------------------------|-------------------------------|
| Name  | string | Producer company name.                     | Marvel Studios                |

### Crew:
| Field | Type   | Description                              | Example                       |
|-------|--------|------------------------------------------|-------------------------------|
| Role  | string | Role of the crew member on the platform. | Director                      |
| Name  | string | Name of the crew member.                 | Joe Russo                     |

### Packages:
| Field      | Type   | Description                                         | Example                       |
|------------|--------|-----------------------------------------------------|-------------------------------|
| Type       | string | Type of business model (transaction-vod, subscription-vod, validated-vod, tv-everywhere, free-vod). | transaction-vod               |
| Definition | string | Video resolution for the package (optional, HD, SD, 4K, 8K). | HD                            |
| BuyPrice   | number | Price for purchasing the content (optional).        | 9.99                          |
| RentPrice  | number | Price for renting the content (optional).           | 3.99                          |
| Currency   | string | Currency code (optional, ISO 4217).                 | USD                           |
| License    | array  | License types (optional, VOD, EST).                | VOD                           |
| Plan       | string | Special subscription including this content (optional). | Premium Subscription          |

### Seasons:
| Field     | Type   | Description                                         | Example                       |
|-----------|--------|-----------------------------------------------------|-------------------------------|
| Number    | integer| Season number (optional).                           | 1                             |
| Episodes  | integer| Number of episodes available for that season (optional). | 10                            |
| Year      | integer| Year of release for the season (optional).          | 2019                          |
| SeasonId  | string | Season ID used by the platform (optional).          | s01                           |
| Title     | string | Title of the season.                                | Season 1                      |
| Deeplink  | string | Deeplink for the season (optional).                | https://www.example.com/season1 |
| OtherIds  | array  | Other identifiers for the season.                  |                             |
| Packages  | array  | Business models available within the season.        |                             |
