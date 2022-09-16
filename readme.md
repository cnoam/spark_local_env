Use the instructions here to run your own environment of Spark + Kafka on you local (Window/Mac/Linux) machine.

This installation uses Spark version 2.4.4

Instead of complicated installs, you will use a ready-made package called *docker container*.
All you have to do is install the program that will run the *containers*, and a few supporting tools.

The program to run the container is called **Docker**. It is possible to use it from command line or as a GUI tool called Docker Desktop.<br>
Even if using the DockerDesktop, you still have to do some operations from the command line.

The plan:
1. install Docker (in Windows, also install [WSL2](https://docs.microsoft.com/en-us/windows/wsl/install) )
2. get Spark+Kafka (will be done automatically when calling `run`)
3. [only once] upload data into the kafka server.
4. use Jupyter notebook (opened automagically by the `run`)
5. Run you code, debug, run... until happy.
6. convert (by copy/paste) the notebook into a python file, and submit to the cluster

# Installing 
**Windows**:<br>
   install Docker Desktop. <Br>
   install WSL2 as detailed in the instructions on the web<br>

**linux/mac**: <br>
  install docker + docker-compose: `sudo apt install -y docker docker-compose`
<hr>    

Open a shell (in Windows, search "ubuntu")

Install this repo:<br>
`git clone https://github.com/cnoam/spark_local_env.git` <br>
`cd spark_local_env`

Run the command: `./run` that internally runs `docker-compose up -d` and start a browser with the jupyter notebook

Import some data into the kafka server now running in your machine. <br>
In a linux console: <br>
```
   sudo apt update
   sudo apt upgrade -y
   sudo apt install kafkacat unzip -y
   unzip static_data.zip
   kafkacat -b localhost:9092 -t activities -P  -l Static\ data/data.json
```   
You now have the data loaded into kafka's storage.
It will be available even after you turn off the service.
 


# Running

The script `run` started the service, and opened the browser for you, ready to play in Jupyternotebook.

If you did not use `run`, you can find the token  printed in the log output of spark.  (you need it to enter the notebook)

*After* the spark session is created, open  http://localhost:4040 to see details on stages, environment etc. This link is exposed by the session and does not exist before the spark session is ready.

load the sample code from the *work* folder and run it. It should succeed and show
```
546083 records in frame
+-------------+-------------------+--------+-----+------+----+-----+-------------+-------------+-------------+
| Arrival_Time|      Creation_Time|  Device|Index| Model|User|   gt|            x|            y|            z|
+-------------+-------------------+--------+-----+------+----+-----+-------------+-------------+-------------+
|1424686735175|1424686733176178965|nexus4_1|   35|nexus4|   g|stand| 0.0014038086|    5.0354E-4|-0.0124053955|
|1424686735378|1424686733382813486|nexus4_1|   76|nexus4|   g|stand|-0.0039367676|  0.026138306|  -0.01133728|
...
```

If the code runs but the output table is empty, you forgot to load data into kafka.


# Stopping
run `docker-compose down` or use the Docker Desktop

All your data is still saved and can be used the next run

# Uninstalling
## linux/mac
```
  $ docker-compose down
  $ docker kill `docker ps -aq`
  $ docker rm `docker ps -aq`
  $ docker rmi `docker images`
```
Now you can uninstall docker itself:
`sudo apt remove docker`
  
## Windows
Same as above + uninstall Docker Desktop


# Troubleshooting

* If you see an error similar to "ERROR: for spark_local_env_kafka_1  Cannot start service kafka: driver failed programming external connectivity on endpoint spark_local_env_kafka_1", restart the computer. This is a bug in docker that keeps older processes hanging
 
* (unverified report from Mac OS): <br>
Replace in file 'run': <br>
`spark_local_env_spark_1` with `spark_local_env-spark-1`

* The linux installation was tested on Ubuntu 22.04 . On Fedora, see https://rmoff.net/2020/04/20/how-to-install-kafkacat-on-fedora/  (Read to the end)


