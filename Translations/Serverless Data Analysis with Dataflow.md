# LAB: Serverless Data Analysis with Dataflow: A Simple Dataflow Pipeline (Java)

## Objectives

In this lab you will learn how to:
 - Setup a Java Dataflow project using Maven

 - Write a simple pipeline in Java
 
 - Execute the query on the local machine
 
 - Execute the query on the cloud


## Steps:
1. Setup a Java Dataflow project using Maven
- Create a bucket with project id, storage class and location

             gsutil mb -p 
             PROJECT_ID c 
             Multi-Regional -l 
             us-central1 -b on gs://
             BUCKET_NAME

- Verify if the bucket exists with echo command.

            BUCKET="<your unique bucket name (Project ID)>"

            echo $BUCKET

- Clone repo and access the folder

            git clone https://github.com/GoogleCloudPlatform/training-data-analyst
    
            cd ~/training-data-analyst/courses/data_analysis/lab2

- Create a dataflow project using maven

             mvn archetype:generate 
            -DarchetypeArtifactId=google-cloud-dataflow-java-archetypes-starter 
            -DarchetypeGroupId=com.google.cloud.dataflow 
            -DgroupId=com.example.pipelinesrus.newidea 
            -DartifactId=newidea 
            -Dversion="[1.0.0,2.0.0]" 
            -DinteractiveMode=false

2.  Write a simple pipeline in Java
- Pipeline filtering

            cd ~/training-data-analyst/courses/data_analysis/lab2/javahelp/src/main/java/com/google/cloud/training/dataanalyst/javahelp/
            nano Grep.java

3.  Execute the query on the local machine
- Run the following command

               cd ~/training-data-analyst/courses/data_analysis/lab2
                export PATH=/usr/lib/jvm/java-8-openjdk-amd64/bin/:$PATH
                cd ~/training-data-analyst/courses/data_analysis/lab2/javahelp
                mvn compile -e exec:java \
                -Dexec.mainClass=com.google.cloud.training.dataanalyst.javahelp.Grep

- Check output

                cat /tmp/output.txt

        
 
4.  Execute the query on the cloud

- Copy some files to the cloud

                gsutil cp ../javahelp/src/main/java/com/google/cloud/training/dataanalyst/javahelp/*.java gs://$BUCKET/javahelp

- In the editor navigate to 

                cd ~/training-data-analyst/courses/data_analysis/lab2/javahelp/src/main/java/com/google/cloud/training/dataanalyst/javahelp

- Replace the input and outputPrefix to

                String input = "gs://qwiklabs-gcp-your-value/javahelp/*.java";
                String outputPrefix = "gs://qwiklabs-gcp-your-value/javahelp/output";

- Examine the script using 

                cd ~/training-data-analyst/courses/data_analysis/lab2/javahelp
                cat run_oncloud1.sh

- Then submit the Dataflow to the cloud

                bash run_oncloud1.sh $DEVSHELL_PROJECT_ID $BUCKET Grep

                



    
