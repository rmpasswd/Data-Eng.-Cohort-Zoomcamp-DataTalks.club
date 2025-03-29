## Linux ft. GCP and VSCode on Windows :)

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
I unchecked 'install python'.
So add another environent variable '' to add our existing python installed path(run `where python` in cmd)  
![image](https://github.com/user-attachments/assets/6ef856bb-737a-409c-8e6c-7486b66501a5)  
If you type in gcloud in your vscode's terminal(ctrl+`), it wont work, need to restart vscode itself.  
![image](https://github.com/user-attachments/assets/3e0e17ab-bbfd-4842-8584-71cbe4c2da03)  
A new entry has been made:  
![image](https://github.com/user-attachments/assets/6c96f18e-3c52-41bd-9032-9cc6ffc3ab1d)  
But on clicking connect and choosing 'linux' this error:  
![image](https://github.com/user-attachments/assets/3b766fa1-1590-49d6-9617-405cdb12adaf)


(Need to run `gcloud compute config-ssh` after restarting gcp instance.)  

.  
<br>
<br>
<br>

#### **Alternate:**  
Above easy step needs to  install 600MB+ gcp cli, instead generate an ssh config file yourself.  
- in windows terminal:  `ssh-keygen -t rsa -f "C:\Users\Ahmad Mahin\.ssh\GCP_keygen" -C mahin_stu2017`  
- Copy the contents of .pub file 
- Then in GCP, go here:  
![image](https://github.com/user-attachments/assets/37bb3a5c-5123-4e58-8ad0-24d930f1d0b0)  
- click add, paste and click 'save' below.

 
- Compose a ssh **config** file, in windows, make a file in `C:\Users\Ahmad Mahin\.ssh\config`
    
    ```python
    
    Host gcp-manual-ssh
        HostName 34.143.199.1
        User mahin_stu2017
        port 22
        IdentityFile "C:\Users\Ahmad Mahin\.ssh\GCP_keygen"
        
    ```
    
    - Host: just an alias.  
    - HostName: taken from here:  
        
      ![image](https://github.com/user-attachments/assets/bac5f03d-6ab5-4c9e-94c6-c2174c662dcd)

        
    - User: refers to the user inside the VM:  
        
       ![image 1](https://github.com/user-attachments/assets/4e9c6649-6f46-47db-9c85-07b05438e9dc)

        
    - IdentityFile: the private key when generated from ssh-keygen command  
    
    - Save, you can later access this file from here:  
    ![image](https://github.com/user-attachments/assets/4cc8a7c9-eee0-4dbe-b132-8dc1cb2ee8d6)
        
    - Use either of these 2 buttons to connect:  
    ![image](https://github.com/user-attachments/assets/c062c8f3-a0b2-4284-b2ad-7395c2c4a2f0)

