## 1. build GCP VM
    ```
    $ sudo apt-get update
    $ sudo apt-get install htop
    $ sudo apt-get install curl -y
	$ curl -sSL https://get.docker.com/ | sh
	$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
	$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
	$ sudo apt-get update 
	$ apt-cache policy docker-ce
	```
## 2.  Install docker mqtt
    ```
    $ sudo sudo mkdir -p /mosquitto/{config,data,log}	
    $ sudo docker run -it -p 1883:1883 -p 9001:9001 --name mqtt eclipse-mosquitto
    ```

## 3. Install docker node-red
    ```
    $ sudo docker login   --> your docjer HUB account
    $ sudo docker pull minihant/hant:1.0.1
    $ sudo docker run -p 1880:1880 --name node minihant/hant:1.0.1
    ```
    - find local host IP
    ```
    $ cat /etc/hosts  --> the ip is at line # Added by Google
    ```
    
