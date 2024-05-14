
Historical Data:
    There is data since 2023-04-03 (year 2023 week 14) to present. 
    Data since 2023-04-03 to 2023-07-10 (year 2023 week 28) has no CDB score (collaborative database views), and since 2023-07-17 
    (year 2023 week 29) to present CDB score is present.

Deleted variables:
    Scores source TMDB: Some tmdb scores were not credibly, there are strange titles with high score.
    Scores source TmdbRaw
    Scores source GoogleTrends: Google trends server is not stable so there are weeks with no data.
    Scores source GoogleTrendsRaw
    Week -> Rename as "WeekOn"
    Genres -> It was a genres array, now it is the primary genre.

Added variables:
    WeekOn: week number of the year corresponding to the date the data is processed (1 to 52/53) (previously "week" field).
    YearOn: year corresponding to the date the data is processed.
    Year: year when the movie/serie was released, coming from IMDB.
    Genre: title primary genre, most common genre in collaborative databases.
    Scores source Cdb: normalized number of visits in last week from collaborative databases (some websites are filmaffinity, letterboxd, sensacine).
    Scores source CdbRaw: raw Cdb score.
    DeltaPositionInt: position change from previous week to current, if title wasn't in previous week data, is null (previously "PreviousPositionChange" field).
    Average: Hits score average inside corresponding Country and Type.
    HitsRelative: (Hits score / Average)-1 , compare Hits score over Average, "how many times is Hits score over Average".
    HitsLocal: Compare Hits score to the Hits score of the same title in its origin country. 
                When Country is title origin country then HitsLocal is 100, 
                if this title hast a better Hits score in another country then HitsLocal will be higher than 100,
                if this title has a worse Hits score in another country then HitsLocal will be lower than 100.
    ReleaseDate: title release date in corresponding country.
    HitsCategory: category assigned to a title according to its Hits score ('Below Average'/'Average'/'Above Average'/'Outstanding'/'Unicorn').
    TrendScore: Hits score growth using last 3/4/5 consecutive weeks.
    TrendCategory: category assigned to a title according to its 'trend_score' score ('Negative Trend'/'Unchanging'/'Slight Trend'/'Average Trend'/'Trend'/'Strong Trend'/'Unicorn').

Hits Score:
    Is the weighted average of the different sources. 
    There are different weights when setting Hits for global scores and when setting Hits for countries, and before and after 2023-07-17.
    
    Before 2023-07-10 (year 2023 week 28) -included- , data with no CDB scores:
        Global weights:
            30% Imdb: Votes
            30% Piracy
            25% Twitter
            15% Youtube
        Countries weights:
            31% Imdb: Votes
            26% Piracy
            26% Twitter
            17% Youtube

    Before 2023-07-17 (year 2023 week 29) -included-  , data with CDB scores:
        Global weights:
            25% Imdb: Votes
            25% Piracy
            20% Twitter
            15% Cdb: Collaborative DB Views
            15% Youtube
        Countries weights:
            25% Imdb: Votes
            20% Piracy
            20% Twitter
            20% Cdb: Collaborative DB Views
            15% Youtube
