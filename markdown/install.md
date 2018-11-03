# 下载安装

在学习Spark之前，免不了需要手动下载Spark源码，手动编译，配置环境等步骤。这里介绍一下必要的步骤，注意下面说的是编译Spark源码的步骤，不是在集群安装部署Spark的步骤。

本地环境依赖：
* Java >= 1.7
* Scala >= 2.0
* Maven >= 2.0

如果不确定本地环境是否安装好，可以在命令行里面用下面的命令查看。
```shell
$ java -version
java version "1.8.0_181"
Java(TM) SE Runtime Environment (build 1.8.0_181-b13)
Java HotSpot(TM) 64-Bit Server VM (build 25.181-b13, mixed mode)

$ scala
Welcome to Scala 2.12.7 (Java HotSpot(TM) 64-Bit Server VM, Java 1.8.0_181).
Type in expressions for evaluation. Or try :help.

$ mvn -v
Apache Maven 3.5.4 (1edded0938998edf8bf061f1ceb3cfdeccf443fe; 2018-06-18T02:33:14+08:00)
Maven home: D:\xxx\apache-maven-3.5.4
Java version: 1.8.0_181, vendor: Oracle Corporation, runtime: C:\Program Files\Java\jdk1.8.0_181\jre
Default locale: zh_CN, platform encoding: GBK
OS name: "windows 10", version: "10.0", arch: "amd64", family: "windows"
```

之后去下载Spark源码(http://spark.apache.org/downloads.html)，注意选Source Code，也可以去GitHub(https://github.com/apache/spark)下载，但有时候不是最新的。

然后去命令行运行下面的命令即可，看到最后BUILD SUCCESS就说明编译成功了。

```shell
$ mvn -DskipTests clean package

# 如果用maven3，还可以用mvn -T 1C -DskipTests clean package这样利用计算机的多核编译的快一些。
....

[INFO] Reactor Summary:
[INFO]
[INFO] Spark Project Parent POM 2.3.2 ..................... SUCCESS [  3.147 s]
[INFO] Spark Project Tags ................................. SUCCESS [  6.727 s]
[INFO] Spark Project Sketch ............................... SUCCESS [ 17.789 s]
[INFO] Spark Project Local DB ............................. SUCCESS [  9.982 s]
[INFO] Spark Project Networking ........................... SUCCESS [ 15.370 s]
[INFO] Spark Project Shuffle Streaming Service ............ SUCCESS [  8.308 s]
[INFO] Spark Project Unsafe ............................... SUCCESS [ 21.072 s]
[INFO] Spark Project Launcher ............................. SUCCESS [ 16.998 s]
[INFO] Spark Project Core ................................. SUCCESS [02:48 min]
[INFO] Spark Project ML Local Library ..................... SUCCESS [ 36.437 s]
[INFO] Spark Project GraphX ............................... SUCCESS [01:06 min]
[INFO] Spark Project Streaming ............................ SUCCESS [01:59 min]
[INFO] Spark Project Catalyst ............................. SUCCESS [03:34 min]
[INFO] Spark Project SQL .................................. SUCCESS [03:16 min]
[INFO] Spark Project ML Library ........................... SUCCESS [03:40 min]
[INFO] Spark Project Tools ................................ SUCCESS [  5.910 s]
[INFO] Spark Project Hive ................................. SUCCESS [02:42 min]
[INFO] Spark Project REPL ................................. SUCCESS [ 31.506 s]
[INFO] Spark Project Assembly ............................. SUCCESS [  4.707 s]
[INFO] Spark Integration for Kafka 0.10 ................... SUCCESS [ 41.663 s]
[INFO] Kafka 0.10 Source for Structured Streaming ......... SUCCESS [01:13 min]
[INFO] Spark Project Examples ............................. SUCCESS [ 51.533 s]
[INFO] Spark Integration for Kafka 0.10 Assembly 2.3.2 .... SUCCESS [  6.360 s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 14:45 min (Wall Clock)
[INFO] Finished at: 2018-11-02T20:53:08+08:00
[INFO] ------------------------------------------------------------------------

```

最后说一点小的提醒，如果在Windows下进行手动编译的话，用自带的命令行工具CMD会编译失败，最好用支持Shell的命令行工具编译，比如Git Bash工具就行。OS X和Linux下没有这种问题。

