# AWS S3 Object Listing & Download Script

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
