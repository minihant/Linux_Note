﻿# Linux install Nodejs

    ```
    apt-get remove nodered -y
    apt-get remove nodejs nodejs-legacy -y
    apt-get remove npm  -y # if installed npm
    curl -sL https://deb.nodesource.com/setup_11.x | sudo bash -
    apt-get install  nodejs-legacy  -y
    node -v
    ```

