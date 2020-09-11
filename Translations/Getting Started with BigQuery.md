# LAB: Getting Started with BigQuery

## Objectives:

In this lab you will learn how to:
 - Load data from Cloud Storage into BigQuery

 - Perform a query on the data using the bq command

## Steps:

1.Load data from Cloud Storage into BigQuery

- Create Dataset with id - logdata with location - US.

                bq --location=US mk -d \
                logdata

- Create Table

                bq mk \
                -t \
                logdata.accesslog

- Load the csv into accesslog

                bq load \
                --autodetect \
                --source_format=CSV \
                logdata.accesslog \
                gs://cloud-training/gcpfci/access_log.csv

2. To query the data from the commandline

                bq query "select string_field_10 as request, count(*) as requestcount from logdata.accesslog group by request order by requestcount desc"


