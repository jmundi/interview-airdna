1. **Set your SPARK_HOME.Version of Spark should be 3.2.0**
   export SPARK_HOME="/path/to/spark"

2. **Create Base Folder**
   mkdir interview
   **copy amenities.txt and properties.json to this directory**

3. **Clone Repository**
   cd interview
   git clone https://github.com/jmundi/interview-airdna

4. **SBT Clean**
   cd interview-airdna
   sbt clean
   sbt assembly
  
5. **Copy generated jar file "interview-airdna-assembly-0.1.jar "from target directory to interview directory.**

6. **From Interview directory, run the following shell command for Ingestion:**
   $SPARK_HOME/bin/spark-submit \
   --master local \
   --deploy-mode client \
   --class org.interview.airdna.IngestJob \
   interview-airdna-assembly-0.1.jar amenities.txt properties.json

7. **From Interview directory, run the following shell command for Reporting:**
   $SPARK_HOME/bin/spark-submit \
   --master local \
   --deploy-mode client \
   --class org.interview.airdna.IngestAudit \
   interview-airdna-assembly-0.1.jar

8. **From Interview directory, run the following shell command for Reporting:**
   $SPARK_HOME/bin/spark-submit \
   --master local \
   --deploy-mode client \
   --class org.interview.airdna.ExportJob \
   interview-airdna-assembly-0.1.jar