## Linux ft. GCP

Turn on GCP VM Instance, then SSH and run commands:
```
mkdir spark && cd spark
wget https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.2_linux-x64_bin.tar.gz
tar xzfv openjdk-11.0.2_linux-x64_bin.tar.gz
export JAVA_HOME="${HOME}/spark/jdk-11.0.2"
export PATH="${JAVA_HOME}/bin:${PATH}"
```
![image](https://github.com/user-attachments/assets/829eac49-7d5b-4958-af6d-0d4b5dd94672)

```
wget https://archive.apache.org/dist/spark/spark-3.0.3/spark-3.0.3-bin-hadoop3.2.tgz
tar xzfv spark-3.0.3-bin-hadoop3.2.tgz
export SPARK_HOME="${HOME}/spark/spark-3.0.3-bin-hadoop3.2" && export PATH="${SPARK_HOME}/bin:${PATH}"

# Test if spark shell works, using scala code:
spark-shell
val data = 1 to 10000
val distData = sc.parallelize(data)
distData.filter(_ < 10).collect()
```
![image](https://github.com/user-attachments/assets/7cefdb30-7fb6-4329-be20-81318151411a)

