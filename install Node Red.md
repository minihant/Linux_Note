# Install Node-js
## for Windows
        1. install nodejs , npm
        ```
         npm install -g --unsafe-perm node-red
         ```
        2. run node-red : c:\node-red
        3. open browser and input : http://127.0.0.1:1880

## [ AWS ] 在 EC2 安裝 Node-RED
        1. 登入到 AWS 
                https://aws.amazon.com/tw/
        2. 啟用與設定 EC2
                2.1  點選上方 【 Services 】 ➙ 點選 【 EC2 】
                2.2  點選 【 Launch Instance 】
                2.3  點選 【 Ubuntu Server 14.04 】 旁邊的 【 Select 】
                2.4  點選 【 t2.micro 】 的 Instance Type
                2.5  點選 【 6.Configure Security Group 】
                - 點選下方的 【 Add Rule 】
                - 在 【 Type 】 欄位中選擇 【 Custom TCP 】
                - 在 【 Port Range 】 欄位中輸入 【 1880 】
                - 在 【 Source 】 欄位中輸入 【 0.0.0.0/0 】
                - 點選 【 Review and Lanuch 】 按鈕
                - 點選 【 Lanuch 】 按鈕
                - 建立 Key
                - 點選 【 Create a new key pair 】 按鈕
                - 在 【 Key pair name 】 欄位輸入一個名稱，例如：ec2-node-red
                - 點選 【 Download Key Pair 】 按鈕
                - 點選 【 Launch Instances 】 按鈕
                - 點選 【 View Instances 】 按鈕
                - 建立完成畫面
        3. 安裝 Node-RED    
                3.1  登入到 EC2  
                3.2  在終端機執行下方指令以安裝 Node-RED
                ```
                  curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
                  sudo apt-get install -y nodejs build-essential
                  sudo npm install -g node-red
                  node-red 
                  ```
                3.3  執行成功畫面   
        4. Run Node-red
                4.1 http://<your-instance-ip>:1880
                4.2 To get Node-RED to start automatically 
                whenever your instance is restarted, you can use pm2:   
                ```                
                sudo npm install -g pm2
                pm2 start `which node-red` -- -v
                pm2 save
                pm2 startup
                ```

## [ GCP ] 在 VM 安裝 Node-RED  
        1. Same as AWS
        2. 防火牆規則建立
                2.1 allow node-red in  : TCP:1880 
                2.2 allow node-red out : TCP:1880
                2.3 allow MQTT-red in  : TCP:1883 
                2.4 allow MQTT-red out : TCP:1883

        3. Set autorun when GCP server start 
        ```       
        $ cp node-red.service to /etc/systemd/system
        $ sudo systemctl enable node-red
        $ sudo systemctl stop node-red
        ```
        
