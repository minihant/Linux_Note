## 1. 更新系統
  ```
  $ sudo apt-get update
  $ sudo apt-get upgrade
  ```

## 2. 安裝 dependency lib Gnome
  ```
  $ sudo apt-get install ubuntu-desktop gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal
  $ $ sudo apt-get install gnome-core
  ```
//-------------------------------------------
## 3. 安裝 VNC Server
  ```
  $ sudo apt-get install vnc4server
  ```

  ### 3.1. 安裝完成後先執行vncserver，會先跳出password設定的選項：
  ```
  $ vncserver  
  ```
  
## 4. 設定vnc config
  修改~/.vnc/xstartup 的設定，加入下面4行:
  ```
    gnome-panel &
    gnome-settings-daemon &
    metacity &
    nautilus &
  ```
    
  ###4.1 殺掉目前執行的vncserver 然後重新執行：
  ```
  $ vncserver -kill :1
  vncserver預設是執行在port 5900上，如果在後面加上：1 就是5901以此類推
  ```
  ### 4.2  啟動 vncserver
  ```
  $ vncserver :1
  ```

## 5. 設定reboot的時候自動執行vncserver
  ```
  $ crontab -e
  select vim editor , 插入reboot資訊於最下方
    @reboot /usr/bin/vncserver :1
    
  編輯完後儲存並重啓伺服器測試
  ```
## //-- install RDP------------------------------------- 
 or install Remote desktop : 
 ```
  $ sudo apt-get install -y xrdp
  $ sudo apt-get install -y xfce4
  $ sudo service xrdp restart
```  
//------------------------------------------------
## install teamviewer
```
$ sudo apt install gdebi-core
$ sudo wget https://download.teamviewer.com/download/linux/teamviewer_amd64.deb
$ sudo sudo gdebi teamviewer_amd64.deb
```
