# PandaS3

This repository contains an open source package for integrating Pandas dataframes with S3 storage and S3 select. The purpose of this library is to enable seamless storage and retrieval of .csv files from S3 from a Pandas DataFrame Object.

## Where to get it
The source code is currently hosted on GitHub at:
https://github.com/Porter97/Pandas3

## How to install
Installers for the latest released version are available at the [Python
package index](https://pypi.org/project/Pandas3)

```sh
# PyPI
pip install pandas3
```

## How To Use It
```
import pandas3
import pandas as pd

# Initialize the client, this starts a boto3 S3 session
pds3 = pandas3.Client('aws-access-key-id', 'aws-secret-access-key', 'region-name')

# Uses S3 session to return all buckets in S3 account, includes request metadata
all_buckets = pds3.list_buckets()

# Parse and retrieve a bucket to list all files. Takes the name of the target bucket as an arg.
files_in_bucket = pds3.list_files(all_buckets['Buckets'][(index of bucket you wish to select']['Name']

# Upload a dataframe to S3
d = {'col1': [1, 2], 'col2': [3, 4]}
df = pd.DataFrame(data=d)

# Upload has a default compression (set to GZIP)
client.upload_df('target-bucket-name', df, 'test-df', compression=True) 

```

## Next Steps
Current there is a utils.py file that includes the basics of string manipulation in order to retrieve stored .csv files (as well as compressed .gz) using S3 Select using basic SQL syntax. S3 Select is also able to access JSON documents too. Under the Client class there is a static method that will be used for using this functionality. The goal here is to have the script upload .csv/.gz/JSON documents into S3 Select, so they can be queried later. There are specific use cases to be handled after this is done.
