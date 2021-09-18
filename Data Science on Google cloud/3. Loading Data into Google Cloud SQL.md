# Loading Data into Google Cloud SQL

### Oevrview
In this lab, you will learn how to import data from CSV text files into Cloud SQL and then carry out some basic data analysis using simple queries.

### Objectives:
* Create Cloud SQL instance
* Create a Cloud SQL database
* Import text data into Cloud SQL
* Build an initial data model using queries

## Clone Repository From Github
In Cloud Shell enter the following commands to clone the repository:
```
git clone \
   https://github.com/GoogleCloudPlatform/data-science-on-gcp/
```
Change to the repository directory:
```
cd data-science-on-gcp/03_sqlstudio
```
Create environment variables that will be used later in the lab for your project ID and the storage bucket that will contain your data:
```
export PROJECT_ID=$(gcloud info --format='value(config.project)')
export BUCKET=${PROJECT_ID}-ml
```

## Create a Cloud SQL instance
We must create instance first, use this command on cloud bash:
```
gcloud sql instances create flights \
    --tier=db-n1-standard-1 --activation-policy=ALWAYS
```
Set a root password for the Cloud SQL instance:  
When prompted for the password type Passw0rd and press enter this will update root password.
in this code we use further password like Passw0rd.
```
gcloud sql users set-password root --host % --instance flights \
 --password Passw0rd
```
Now create an environment variable with the IP address of the Cloud Shell and Allowlist the Cloud Shell instance for management access to your SQL instance with this command:
```
export ADDRESS=$(wget -qO - http://ipecho.net/plain)/32
gcloud sql instances patch flights --authorized-networks $ADDRESS
```
When prompted press Y to accept the change.

## Get Your CLOUD SQL IP Adress
Run this code to get your IP Adress
```
MYSQLIP=$(gcloud sql instances describe \
flights --format="value(ipAddresses.ipAddress)")
echo $MYSQLIP
```
Create table using create_table.sql file:
```
mysql --host=$MYSQLIP --user=root \
      --password --verbose < create_table.sql
```
When prompted for a password enter Passw0rd.

## Enter Mysql Command Line Interface
```
mysql --host=$MYSQLIP --user=root  --password
```
Type the password that you use
