# Introduction to Google Cloud Dataflow
This file contains text you can copy and paste for the examples in Cloud Academy's _Introduction to Google Cloud Dataflow_ course.  

### Building and Running a Simple Pipeline
Installing on your own computer: https://cloud.google.com/dataflow/docs/quickstarts  
Transforms: https://beam.apache.org/documentation/sdks/javadoc/2.0.0/org/apache/beam/sdk/transforms/package-summary.html

```
cd beam/examples/java8
mvn compile exec:java -Dexec.mainClass=org.apache.beam.examples.LineCount
```
```
gsutil cat gs://dataflow-samples/shakespeare/kinglear.txt | wc
```

### Deploying a Pipeline on Cloud Dataflow
```
cd ~/beam/examples/java8
PROJECT=[Your Project ID]
BUCKET=gs://dataflow-$PROJECT
gsutil mb $BUCKET
```
```
mvn compile exec:java -Dexec.mainClass=org.apache.beam.examples.LineCount \
  -Dexec.args="--project=$PROJECT \
  --stagingLocation=$BUCKET/staging/ \
  --output=$BUCKET/output \
  --runner=DataflowRunner \
  --jobName=linecount1"
```
