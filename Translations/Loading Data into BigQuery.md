# LAB: Loading data into BigQuery

## Objectives:

In this lab you will learn how to:
 - Create a new dataset to store tables

 - Ingest a new Dataset from a CSV

 - Ingest a new Dataset from Google Cloud Storage

 - Create Tables from other tables


## Steps

1. Create Dataset with id - nyctaxi with location - US.

            bq --location=us mk -d \  
            nyctaxi

2. Ingest a new Dataset from CSV

            bq --location=us
            load \
            --source_format=
            CSV \
            PROJECT_ID:nyctaxi.2018trips \
            C:\Users\USER\Downloads\nyc_tlc_yellow_trips_2018_subset_1.csv \
            --autodetect

3. Ingest a new Dataset from Google Cloud Storage

            bq load \
            --source_format=CSV \
            --autodetect \
            --noreplace  \
            nyctaxi.2018trips \
            gs://cloud-training/OCBL013/nyc_tlc_yellow_trips_2018_subset_2.csv

4.  Create Tables from other tables with DDL

- To create table of only January trips with the dataset

            bq query \
            --destination_table nyctaxi.januaryTable \
            --use_legacy_sql=false \
            'FROM
              nyctaxi.2018trips
            WHERE
              EXTRACT(Month
              FROM
                pickup_datetime)=1'

- To find the longest distance travelled

            bq query --nouse_legacy_sql \
            'SELECT
              *
            FROM
              nyctaxi.january_trips
            ORDER BY
              trip_distance DESC
            LIMIT
              1







