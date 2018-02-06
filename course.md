# Introduction to Google Cloud Dataflow
This file contains text you can copy and paste for the examples in Cloud Academy's _Introduction to Google Cloud Dataflow_ course.  

### Building and Running a Pipeline
Installing on your own computer: https://cloud.google.com/dataflow/docs/quickstarts  
Transforms: https://beam.apache.org/documentation/sdks/javadoc/2.0.0/org/apache/beam/sdk/transforms/package-summary.html

```
git clone https://github.com/rathihimanshu/beam.git
cd beam/examples/java8
mvn compile exec:java -Dexec.mainClass=org.apache.beam.examples.MinimalLineCount
```
```
gsutil cat gs://dataflow-samples/shakespeare/kinglear.txt | wc
```

### Deploying a Pipeline on Cloud Dataflow
```
nano ~/.profile
    PROJECT=[Your Project ID]
    BUCKET=gs://dataflow-$PROJECT
gsutil mb $BUCKET
cd ~/beam/examples/java8
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
cd ~/beam/examples/java8
```
```
mvn compile exec:java -Dexec.mainClass=org.apache.beam.examples.MinimalWordCount \
  -Dexec.args="--runner=DataflowRunner \
  --project=$PROJECT \
  --tempLocation=$BUCKET/temp \
  --output=$BUCKET/wordcounts"
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

### Windowing
```
cd ~/beam/examples/java8
```
```
mvn compile exec:java -Dexec.mainClass=org.apache.beam.examples.complete.game.HourlyTeamScore \
-Dexec.args="--runner=DataflowRunner \
  --project=$PROJECT \
  --tempLocation=$BUCKET/temp/ \
  --output=$BUCKET/scores \
  --startMin=2015-11-16-16-00 \
  --stopMin=2015-11-17-16-00"
```

### Running LeaderBoard
```
bq mk game
```
API Console Credentials: https://console.developers.google.com/projectselector/apis/credentials
```
export GOOGLE_APPLICATION_CREDENTIALS="[Path]/[Credentials file]"
cd ~/beam/examples/java8
```
```
mvn compile exec:java  -Dexec.mainClass=org.apache.beam.examples.complete.game.injector.Injector \
-Dexec.args="$PROJECT game none"
```
```
cd ~/beam/examples/java8
```
```
mvn compile exec:java -Dexec.mainClass=org.apache.beam.examples.complete.game.LeaderBoard \
-Dexec.args="--runner=DataflowRunner \
  --project=$PROJECT \
  --tempLocation=$BUCKET/temp/ \
  --output=$BUCKET/leaderboard \
  --dataset=game \
  --topic=projects/$PROJECT/topics/game"
```
