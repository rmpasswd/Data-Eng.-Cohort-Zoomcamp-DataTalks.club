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

To easily connect to the GCP VM from Vscode:  
from this guide: https://learn.canceridc.dev/cookbook/virtual-machines/using-vs-code-with-gcp-vms  
install the gcp cli: https://cloud.google.com/sdk/docs/install  
Check that gcloud path has been added to windows environment 'path' variable: C:\Program Files (x86)\Google\Cloud SDK\google-cloud-sdk\bin  
We unchecked 'install python'  
Add another environent variable '' to add our existing python installed path(run `where python` in cmd)  
![image](https://github.com/user-attachments/assets/6ef856bb-737a-409c-8e6c-7486b66501a5)  
If you type in gcloud in your vscode's terminal(ctrl+`), it wont work, need to restart vscode itself.  
![image](https://github.com/user-attachments/assets/3e0e17ab-bbfd-4842-8584-71cbe4c2da03)  
A new entry has been made:  
![image](https://github.com/user-attachments/assets/6c96f18e-3c52-41bd-9032-9cc6ffc3ab1d)  
.

