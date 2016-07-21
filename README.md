The helloworld demo is a spark project with maven and java.

1 创建SimpleApp.java文件：

/* SimpleApp.java */

import org.apache.spark.api.java.*;

import org.apache.spark.SparkConf;

import org.apache.spark.api.java.function.Function;

 

public class SimpleApp {

  public static void main(String[] args) {

    String logFile = "YOUR_SPARK_HOME/README.md"; // Should be some file on your system

    SparkConf conf = new SparkConf().setAppName("Simple Application");

    JavaSparkContext sc = new JavaSparkContext(conf);

    JavaRDD<String> logData = sc.textFile(logFile).cache();

 

    long numAs = logData.filter(new Function<String, Boolean>() {

      public Boolean call(String s) { return s.contains("a"); }

    }).count();

 

    long numBs = logData.filter(new Function<String, Boolean>() {

      public Boolean call(String s) { return s.contains("b"); }

    }).count();

 

    System.out.println("Lines with a: " + numAs + ", lines with b: " + numBs);

  }

}

 
2 创建pox文件

<project>

  <groupId>edu.berkeley</groupId>

  <artifactId>simple-project</artifactId>

  <modelVersion>4.0.0</modelVersion>

  <name>Simple Project</name>

  <packaging>jar</packaging>

  <version>1.0</version>

  <dependencies>

    <dependency> <!-- Spark dependency -->

      <groupId>org.apache.spark</groupId>

      <artifactId>spark-core_2.10</artifactId>

      <version>1.6.2</version>

    </dependency>

  </dependencies>

</project>

3 路径

 
4 执行命令

$ /opt/mapr/spark/spark-1.6.1/bin/spark-submit \

  --class "org.sparkexample.SimpleApp" \

  --master local[4] \

  simple-project-1.0.jar

 
 本人博客：http://www.cnblogs.com/rongyux/p/5691669.html
