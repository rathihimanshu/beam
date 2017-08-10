# Introduction to Google Cloud Dataflow
This file contains text you can copy and paste for the examples in Cloud Academy's _Introduction to Google Cloud Dataflow_ course.  

### Deploying a Pipeline Locally
Installing on your own computer: https://cloud.google.com/dataflow/docs/quickstarts  
Transforms: https://beam.apache.org/documentation/sdks/javadoc/2.0.0/org/apache/beam/sdk/transforms/package-summary.html

```
cd beam/examples/java8
mvn compile exec:java -Dexec.mainClass=org.apache.beam.examples.MinimalLineCount
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
mvn compile exec:java -Dexec.mainClass=org.apache.beam.examples.MinimalLineCountArgs \
  -Dexec.args="--runner=DataflowRunner \
  --project=$PROJECT \
  --tempLocation=$BUCKET/temp"
```
```
mvn compile exec:java -Dexec.mainClass=org.apache.beam.examples.LineCount \
  -Dexec.args="--runner=DataflowRunner \
  --project=$PROJECT \
  --tempLocation=$BUCKET/temp \
  --output=$BUCKET/linecount"
```

### Custom Transforms
```
cd ~/beam/examples/java
mvn compile exec:java -Dexec.mainClass=org.apache.beam.examples.MinimalWordCount
```

### Composite Transforms
```
cd ~/beam/examples/java8
```
```
mvn compile exec:java -Dexec.mainClass=org.apache.beam.examples.complete.game.UserScore \
-Dexec.args="--runner=DataflowRunner \
  --project=$PROJECT \
  --tempLocation=$BUCKET/temp/ \
  --output=$BUCKET/scores"
```
