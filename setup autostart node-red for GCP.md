## From inside the VM.  Without that you need to run "gcloud auth login"

1. run form script file:
```
gcloud compute instances create gcp-node-red --metadata-from-file startup-script=/usr/bin/node-red
```
2. Run Providing script contents directly 
```
# === Startup ====================  
gcloud compute instances start gcp-node-red --metadata startup-script="echo 'hello world'"

gcloud compute instances start gcp-node-red --tags noderedstart \
--metadata startup-script='#! /bin/bash

# Installs apache and a node-red
sudo su -
node-red
EOF'
 
   
   
   //=== Shutdown ================= 
   gcloud compute instances create gcp-node-red --metadata shutdown-script="#! /bin/bash
   >  #Shuts down Apache server
   > /etc/init.d/node-red stop"
   
   ==== Connect to instance ==================
   gcloud compute ssh gcp-node-red
```

3. use bash command to auto start
```
$ sudo nano ~/.bashrc
```
     - add “bash start_nr.sh” in the last line 

4. ----使用 forever-------
     - 安裝 forever 來使node 不會因為關掉 ssh 而終止，然後執行 cd 到目錄，使用 forever start -c 來執行原本要指行的命令 
     - install forever
     ```
     $ sudo npm install forever -g
     $ sudo npm install forever-monitor
     $ forever start app.js
     ```
     
