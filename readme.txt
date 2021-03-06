Training Model - wine_training.py
Prediction Model - wine_prediction.py

####### Create an EMR cluster #######

In the AWS console select EMR.
In EMR, select create a cluster.
change Applications to Spark, Number of instances to 4(1 master, 3 slaves) in Hardware Configuration
select your EC2 key pair and create the cluster.

Edit security group configurations for the master.
In inbound rules add SSH with My-IP.

####### Connecting to the Master #######

Connect to the master instance using PuTTY.
You need the public IP address of the master and .pem file to connect to the cluster.
Enter the IP address in Host name.
Session -> SSH -> Auth -> select the .pem file from your local machine.

Transfer the files using WinSCP.
Connect to the master and then drag and drop all the required files.

####### Execution #######

After connecting to the master successfully, run the following commands:

sudo yum install python3
sudo yum install pip
sudo pip3 install wheel
sudo pip3 install pyspark
sudo pip3 install findspark
sudo pip3 install numpy
sudo yum install docker

To execute the code without using docker run the following commands:
$ python wine_training.py TrainingDataset.csv
$ python wine_prediction.py ValidationDataset.csv


To execute the code using docker run the following:
$ export PYSPARK_PYTHON=/usr/bin/python3
$ export PYSPARK_DRIVER_PYTHON=/usr/bin/python3
$ sudo service docker start
$ sudo docker run --name myRandomModel1 -v ValidationDataset.csv --env PYSPARK_PYTHON=/usr/bin/python3 --env PYSPARK_DRIVER_PYTHON=/usr/bin/python3 -it jb779/cloud

