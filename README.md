<p align="center">
<image
  src="https://s3.invisionapp-cdn.com/storage.invisionapp.com/boards/files/183060432.png?x-amz-meta-iv=1&x-amz-meta-ck=cd20ea812f8ae161523111afa5aea5e8&AWSAccessKeyId=AKIAWCDCF6QSLTS7LRWT&Expires=1717200000&Signature=90X61ZsbGe2EneL7IRbEzerj7Oc%3D"
  height=150
  margin=0>
</p>
  
# BB Media
Award Winning Data Science Company, specialized in Media & Entertainment for over 36 years. 
We study how markets evolve in any of their formats and screens, developing primary survey methodologies for linear and non-linear measurement of content.
We are focused. We are experts. We innovate. We act fast. We are thorough. We deliver.

<p align="center">
<image
  src="https://github.com/BB-Media-IT/ClientScriptHub/assets/4085605/46558862-529d-4dec-a7a8-7d956fec88f3"
  height=80
  margin=0>
</p>
  
## Companies thath trust in us
![image](https://github.com/BB-Media-IT/ClientScriptHub/assets/4085605/c2df7aca-cf33-4006-9541-3256c1f97abd)

## BB MEDIA COVERAGE

![image](https://github.com/BB-Media-IT/ClientScriptHub/assets/4085605/8c82551a-5f0c-4fd0-b730-1efb86fd0ed5)

## Data Hub
Welcome to your go-to resource for media insights and data analytics, housed securely in our S3 Data Lake! Our Data Hub serves as a central repository for comprehensive data and in-depth analysis across a spectrum of streaming services and media content. Whether you're diving into market trends, scouting for content availability, or exploring strategic media insights, our Data Hub provides a suite of projects tailored to meet a diverse range of needs within the media landscape.

Here's what you can find in our S3-hosted Data Hub:

- [Streaming Availability](#streaming-availability)
- [Audiovisual Identifier & Metadata](#audiovisual-identifier--metadata)
- [Hits](#hits)
- [Platforms, Plans & Bundles](#platforms-plans--bundles)
- [Platform Essentials](#platform-essentials)
- [Content Tracker & Upcoming Titles](#content-tracker--upcoming-titles)
- [Livestreaming & Fast Channels](#livestreaming--fast-channels)
- [Awards](#awards)
- [Top Ten](#top-ten)

## Streaming Availability
Discover a comprehensive database of movies, series, and episodes available on-demand (OD) in more than 200 regions. Our offering includes a detailed breakdown of business models such as SVOD, AVOD, TVOD, and TVE. ['Content Pulse'](https://bb-media.com/streaming/) provides normalized metadata, while 'Streaming Availability' offers raw data, showcasing how each service communicates its content with universal IDs and enriched with BB Media’s intelligent metadata.

### Features
- On-demand availability across countries and services
- Breakdown by business model: SVOD, AVOD, TVOD, TVE
- Daily and weekly updates of the content offering
- BB UID: a unique identifier for streamlined content tracking
- 
### Updates & Coverage
- Data is updated weekly
- Covers a vast range of countries globally

[Schema, Modeling & Access](https://google.com)

🌟 For more information and pricing details, please feel free to [click here](mailto:hello@bb-media.com?subject=Let's Unlock Amazing Deals Together!)! We'd love to help you.🌟

## Audiovisual Identifier & Metadata

Our advanced algorithm aims to standardize different products by unifying content identifiers, allowing for streamlined metadata across our offerings. Updated weekly, it gathers information from various sources to generate our universal identification code known as BB UID.

### Features
- Standardization of content identifiers
- Streamlined metadata for easy integration
- Weekly updates from various sources
- Generation of BB UID for universal content tracking

For more information on schemas and to access our S3 buckets, please [insert link here].

### Updates & Coverage
- Information is updated on a weekly basis
- Comprehensive collection from multiple sources to ensure accuracy and relevance

For full details on our update schedule and coverage, refer to our General Information Sheet [insert link here].

## Hits
## Platforms, Plans & Bundles
## Platform Essentials
## Content Tracker & Upcoming Titles
## Livestreaming & Fast Channels
## Awards
## Top Ten

## AWS S3 Object Listing & Download Script

This script connects to an S3-compatible storage (like Digital Ocean Spaces) to list and download objects based on certain prefixes.

## Requirements
- Python 3
- `boto3` library
- A configuration file (`config.cfg`) with necessary credentials and parameters.

## Configuration File (`config.cfg`)

The configuration file should have sections and keys for the AWS/Digital Ocean (or any S3-compatible storage) configurations as well as for defining prefixes and download paths. 

Structure:
```
[aws_digital_ocean]
REGION_NAME = Copy the one we provide 
ENDPOINT = Copy the one we provide
ACCESS_ID = Copy the one we provide
SECRET_KEY = Copy the one we provide
BUCKET = Copy the one we provide

[prefix_buckets]
CONTENTS = Content/latest
EPISODES = Episodes/latest
STATS = Stats/latest
SOURCE = Stats/latest

[paths]
CONTENTS = Datos/Contents
EPISODES = Datos/Episodes
STATS = Datos/Stats
SOURCES = Datos/Sources
```

## How It Works

1. **Variable Collection:** The script starts by reading the `config.cfg` file and obtaining the necessary configurations.

2. **Connection Configuration:** The script establishes a connection to the S3 compatible storage.

3. **Pagination Activation:** Uses paginator to list all objects in the specified bucket.

4. **List Prefix:** It lists all objects based on the specified prefixes in the configuration file.

5. **Download Files:** All objects listed will be downloaded to specified paths based on their prefixes. The script ensures that the directories exist; if not, it creates them.

## How to Run
1. Ensure you have the necessary dependencies installed, mainly `boto3`.
2. Update the `config.cfg` file with the required configurations.
3. Run the script.

## Notes
Remember to never commit your `config.cfg` with sensitive credentials to a public repository.

## Schedule
You can create a .sh, .bat, or any required file and run it with an orchestrator or just with a crontab.

Example:
At 12:00 on Saturday: `0 12 * * 6`
