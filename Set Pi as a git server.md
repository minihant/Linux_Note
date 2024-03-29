# Setting up Raspberry Pi as a git server
  ### Reference : https://dev.to/kodaman2/setting-up-raspberry-pi-as-a-git-server-230f

## 1. Enable SSH in pi
  ```
  Enter ' $ sudo raspi-config ' in a terminal window
  Select Interfacing Options 
  Navigate to and select SSH 
  Choose Yes 
  Select Ok 
  Choose Finish 
  ```
## 2. set Static IP in pi
  ```
  $ sudo vim /etc/dhcpcd.conf
    and modify as following formate
    # Example static IP configuration
    interface eth0
    static ip_address=192.168.0.28
    #static ip6_address=fd51:42f8:caae:d92e::ff/64
    static routers=192.168.0.1
    static domain_name_servers=192.168.0.1
  ```
  
## 3. set SSH Port (Optional)  default port: 22
  ```
   $ sudo vim  /etc/ssh/sshd_config 
  ```
   After changing the port:
   ```
   $ sudo service ssh restart
   ```
    
## 4. DNS Setup (Optional) 
    Sign up for an account at NoIP and go through the steps.
    
## 5. USB Drive Mount 
  ```
    $ lsblk or sudo fdisk -l  ### will show disk devices
  ```
    To mount the usb:
  ```
    $ sudo mount /dev/sda1 /mount/path
  ```  
    if you want to format your USB follow the below steps:
    ```
    $ sudo fdisk /dev/sda1 
      # m, for help
      # q, for exit
      # d, to delete partitions, repeat if there are more i.e. sda2, sda3, etc...
      # n, to create new partitions, I did p, and hit enter 4 times.
      # w, to finish
    ```
    
## 6. Try  Clone a PUBLIC repo
  ```
  $ git clone https://github.com/yourAccount/YourRepo.git
  ```
  
## 7. Try Cloning Private Repo from GitHUB
  * Generate SSH Key, when done just cat to it, and paste on github:
  ```
    $ ssh-keygen -t rsa -C "your_email@example.com"
  ```
    cd cd ~/.ssh
    * will have 3 files: id_rsa , id_rsa.pub ,unknown_hosts
    * copy the 3 files into USB drive , and move USB drive to PC and copy to c:/Users/hant/.ssh
  * Add SSH Key to the git Hub
     ref: https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account
     
## 8. Set pi Directory permissions 
  * our folder might need permissions for pi user.
  ```
    $ sudo chown -R pi:pi /your/git/folder
  ```
    
## 9. Add receive.denyCurrentBranch updateInstead in pi
  ```
  $ git config --local receive.denyCurrentBranch updateInstead
  ```
  
## 10. Add pushurl to origin 
### a. in Pi :
    ```
    mkdir /media/pi/USBdriver/newproj
    cd /media/pi/USBdriver/newproj
    $ git init
    ```
### b. in PC:
    ```
    mkdir workDir
    cd WorkDir
    $ vgit clone pi@raspberrypi:/media/pi/WINPOS16G/newproj
    ```
### * now you can begin to add files into this directory
### * after that you can:
      ```
      $ git add .     ## to tag the add/modify files
      $ git commit -m 'your change history message'  ## add change message to commit
      $ git push pi@raspberrypi:/media/pi/WINPOS16G/newproj
         or 
      $git push   
      ```
## 11. Test your setup
