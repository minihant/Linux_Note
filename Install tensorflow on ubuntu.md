# install tensorflow 
  ref : https://www.tensorflow.org/install/pip
//----------------------------------
1. python3 --version
  ```
  $ sudo apt install python3-dev python3-pip
  ```
2. pip3 --version
  ```
    $ sudo apt install python3-pip
  ```  
3. virtualenv --version
  ```
    $ sudo apt install virtualenv
  ```  
4. Create a virtual environment
  ```
  $ virtualenv --system-site-packages -p python3 ./venv
  $ source ./venv/bin/activate  # sh, bash, ksh, or zsh
  $ pip install --upgrade pip
  $ pip list
  ```
5. Install the TensorFlow pip package  
  ```
  $ pip install --upgrade tensorflow
  ```
   //------------------------------------
  Choose one of the following TensorFlow packages to install from PyPI:
  ```
  $ tensorflow —Latest stable release for CPU-only (recommended for beginners)
  $ tensorflow-gpu —Latest stable release with GPU support (Ubuntu and Windows)
  $ tf-nightly —Preview nightly build for CPU-only (unstable)
  $ tf-nightly-gpu —Preview nightly build with GPU support (unstable, Ubuntu and Windows)
  $ tensorflow==2.0.0-beta1 —Preview TF 2.0 Beta build for CPU-only (unstable)
  $ tensorflow-gpu==2.0.0-beta1 —Preview TF 2.0 Beta build with GPU support (unstable, Ubuntu and Windows)
  ```
  
  Verify the install:
  ```
  $ python -c "import tensorflow as tf;print(tf.reduce_sum(tf.random.normal([1000, 1000])))"
  ```
  
  install anoth package : skimage , opencv2
  ```
  $ sudo apt-get install -y libsm6 libxext6 libxrender-dev
  $ pip install scikit-image
  $ pip install opencv-python==      # this will list the available version
  $ pip install opencv-python==4.1.0.25
  $ pip install imgaug
  $ pip install tqdm
  ```
  
//======================================================================  
6. And to exit virtualenv later: 
  ```
  $ deactivate  # don't exit until you're done using TensorFlow
  $ source ./venv/bin/activate tensorflow 
  ```
//===========================================
Training module
//===============================================
1. prepare dataset and make train list:
  ```
  cd k210-face-detection
  wget http://tamaraberg.com/faceDataset/originalPics.tar.gz
  mkdir FDDB
  tar -zxvf originalPics.tar.gz -C FDDB
  wget http://vis-www.cs.umass.edu/fddb/FDDB-folds.tgz
  tar -zxvf FDDB-folds.tgz -C FDDB
  python3 tools/make_list.py --fddb_dir FDDB --ann_dir FDDB/FDDB-folds
  ```
  
2. training
  ```
  $ make train_pureconv ILR=0.001 MAXEP=20 IAA=false
    ILR : the init learning rate
    MAXEP : max epoch
    IAA : whether to use data augmenter
    NOTE: you can use CKPT:xxxxx to continue train
    $ make train_pureconv CKPT=log/20190216-152633 ILR=0.0005 MAXEP=20 IAA=true
  And you can use tensorboard --logdir log to look the record
  ```
3. test model:
  ```
  $ make inference PB=Freeze_save.pb
  ```
  
4. export pb :
  a. freeze ckpt
    ```
    $ make freeze CKPT=log/20190216-154422 
        now your fold will have Freeze_save.pb
    ```
  b. use kendryte-model-complier to complie pb file
        you can use my script (you should modify MODELCMP):
    ```
    $ make kmodel_convert PB=Freeze_save.pb MODELCMP=~/Documents/kendryte-model-compiler
        or refer to see the kendryte-model-compiler:
          https://github.com/kendryte/kendryte-model-compiler
    ```
  
5. modfiy k210 code  :
  a. copy weights array to code
    ```
    $ cp ~/Documents/kendryte-model-compiler/build/gencode_output.* K210_code/
    ```
  b. compile the code
      you can refer to the documents k210 use in windows or k210 use in linux
      And you can find some useful article in my bolg.
  c. down load program now you can use kflash.py down load the program
  
  //---------------------------
  // run tensorflow on jupyter
  //----------------------------
 1. install Anaconda :
  ```
  $ wget Anaconda3-2019.03-Linux-x86_64.sh
  $ chmod +x Anaconda3-2019.03-Linux-x86_64.sh
  $ ./Anaconda3-2019.03-Linux-x86_64.sh
  ```
  
 2. install jupytor notebook
  ```
  $ pip install jupyter
  $ source deactivate tensorflow
 
  $ source activate tensorflow
  $ juypter notebook
  $ open brwoser :  http://localhost:8888
  ```
  ok
  install tensprflow on docker
    ```
    $ docker pull tensorflow/tensorflow                  # Download latest image
    $ docker run -it -p 8888:8888 tensorflow/tensorflow  # Start a Jupyter notebook server 
  ```
