Use the instructions here to run your own environment of Spark + Kafka on you local (Window/Mac/Linux) machine.

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

## Installing 
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
 


## Running

The script `run` started the service, and opened the browser for you, ready to play in Jupyternotebook.

If you did not use `run`, you can find the token  printed in the log output of spark.  (you need it to enter the notebook)

*After* the spark session is created, open  http://localhost:4040 to see details on stages, environment etc. This link is exposed by the session and does not exist before the spark session is ready.

## Stopping
run `docker-compose down` or use the Docker Desktop

All your data is still saved and can be used the next run

## Uninstalling
### linux/mac
```
  $ docker-compose down
  $ docker kill `docker ps -aq`
  $ docker rm `docker ps -aq`
  $ docker rmi `docker images`
```
Now you can uninstall docker itself:
`sudo apt remove docker`
  
### Windows
Same as above + uninstall Docker Desktop
 
