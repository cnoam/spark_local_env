Use the instructions here to run your own local (on your Window/Mac/Linux) machine.

## Installing 
**Windows**:<br>
   install Docker Desktop. <Br>
   install WSL2 as detailed in the instructions on the web<br>
   *note*: compose is already part of Docker Desktop

**linux/mac**: <br>
  install docker + docker-compose: `sudo apt install -y docker docker-compose`
<hr>    

Open a shell (in Windows, search "ubuntu")

Install this repo: `git clone https://github.com/cnoam/spark_local_env.git` <br>
`cd spark_local_env`

Run the command: `./run`   that internally runs `docker-compose up -d` and start a browser on the jupyter notebook

Import some data into the kafka server now running in your machine. <br>
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
 
