Use the instructions here to run your own local (on your Window/Mac/Linux) machine.

## Installing 
1. install Docker Desktop. <Br>
   *Windows*: install WSL as detailed in the instructions on the web
   
1.1 install docker-compose: `sudo apt install docker-compose` or https://docs.docker.com/compose/install/compose-desktop/ <br>
    *Windows*: compose is already part of Docker Desktop
   
2. run the command: `./run`   that internally runs `docker-compose up -d`

3. import some data into the kafka server now running in your machine. <br>
```
   unzip static_data.zip
   sudo apt install kafkacat
   kafkacat -b localhost:9092 -t activities -P  -l Static\ data/data.json
   # rm data.json data.zip # TODO: verify the data persists after killing the container
```   
   


## Running
if the spark server started succesfully in the previous stage, you can now connect using http://localhost:8888 and open jupyter notebook.

The token is printed in the log output of the spark. 

open  http://localhost:4040 to see details on stages, environment etc.

 or just run the script `run` that will start the service, and then open the browser for you.

## Stopping
run `docker-compose down`.

All your data is still saved and can be used the next run

## Uninstalling
### linux/mac
```
  $ docker-compose down
  $ docker kill `docker ps`
  $ docker rm `docker ps -aq`
  $ docker rmi `docker images`
```
Now you can uninstall docker itself:
`sudo apt remove docker`
  
### Windows
TBD
 
