# Setup your google cloud VM
1. Create an account (Will charge your $1 for testing your credit card and returned to you later) 
2. Create your storage bucket (optional)
3. Create a VM instance (select Asia zone will save a lot!) (The following is an VM instance example) 
    - Ubunto 16.10. 
    - 8 cores + 52 GB memory 
    - Standard persistent disk: 150G 
    - (optional) set up your SSH key then you could visit your VM through your local ftp tools (such as putty)
4. Setup swap area (optional): 
    - sudo fallocate -l 50G /swapfile          // Normally use memorysize*2, I set 50G 
    - sudo chmod 600 /swapfile                               //change the file permission 
    - sudo mkswap /swapfile                                  //create swap space 
    - sudo swapon /swapfile                                  //turn-on swap 
    - free –m                                                //check if swap is opened successfully 
    - sudo swapoff /swapfile                                 //turn-off swap 
    - sudo vim /etc/fstab                                              //Add the following at last 
        - /swapfile   none    swap    sw    0   0 
    - sudo sysctl vm.swappiness=10           //vm.swappiness determines using memory or swap, memory(0), swap(100) 
    - sudo sysctl vm.vfs_cache_pressure=50   //default=100, deermines the file exchange frequency 
    - sudo vim /etc/sysctl.conf              //Add following to the last, setup configure when VM is turned on  
        - vm.swappiness=10 
        - vm.vfs_cache_pressure = 50 
5. Use IE connect to new VM (or your putty) 
6. Install all the necessary components: 
    - sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev valgrind cmake unrar gfortran python3-pip python3-dev python3-wheel swig git git-core htop 
7. sudo apt update 
8. sudo apt-get install python-pip python-setuptools 
9. sudo pip install --upgrade pip 
10. Check pip version: pip –version (>9.0) 
11. Install python3 environment: 
    - pip install --upgrade virtualenv 
12. Create a virtual environment 
    - Mkdir your-project-directory 
    - cd your-project-directory 
    - virtualenv --python python3 env 
13. Active/deactive environment:  
    - source env/bin/activate 
    - Deactive 

14. Install all common DS packages in your environment: 
    - pip install numpy scipy matplotlib pandas seaborn sklearn lightgbm xgboost tqdm 

15. *Do not forget to turn off your VM if you do not use it for a long time.*

# Upload and download files to your google VM: 

1. From your google sorage: 
    - Google SDK initially installed, update SDK tools: pip install --upgrade google-cloud-storage 
    - Copy your file between your storage bucket and VM  
        - Gsutil cp gs://your-bucket-name/your-file . 
        - gsutil –o GSUtil:parallel_composite_upload_threshold=150M cp your-bigfile gs://your-bucket/ (for very large file) 

*Using 'gsutil config'  then copy-paste the link to get the authorization code, paste the code and get the permission to white to your storage bucket*
