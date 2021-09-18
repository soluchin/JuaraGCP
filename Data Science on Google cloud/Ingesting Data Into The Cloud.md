# Ingesting Data Into The Cloud
You will learn how to use a bash script to download selected data, which providess historic information about internal flights in the United States.

> **Cloud Shell**
> Access: click Activate Cloud Shell button 

List active account command:
```bash
gcloud auth list
```
List the project ID command:
```bash
gcloud config list project
```
## Retrieving Data From a Website
You will use `curl` to fetch the monthly CSV files that contain the raw data that will be used to build your complete data set. The data set is called the On-Time performance data.
```bash
curl https://www.bts.dot.gov/sites/bts.dot.gov/files/docs/legacy/additional-attachment-files/ONTIME.TD.201501.REL02.04APR2015.zip --output data.zip
```

## Download Custom Data From a Storage Bucket
Snapshots of custom BTS data have been organized and saved in a public storage bucket.
The simplest way to ensure you get the data you need for this lab is to download it from the  `data-science-on-gcp`  public storage bucket. A script is provided in the repo to help achieve this.
```bash
cat ../02_ingest/ingest_from_crsbucket.sh

export PROJECT_ID=$(gcloud info --format='value(config.project)')
gsutil mb gs://${PROJECT_ID}-ml

bash ../02_ingest/ingest_from_crsbucket.sh ${PROJECT_ID}-ml
```

