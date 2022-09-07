Use the instructions here to run your own local (on your Window/Mac/Linux) machine.

Steps:
1. install docker  or docker desktop
1.1 install docker-compose: `sudo apt install docker-compose` or https://docs.docker.com/compose/install/compose-desktop/
2. run the command: docker-compose up -d
3. import some data into the kafka server now running in your machine.
   unzip static_data.zip
   sudo apt install kafkacat
   kafkacat -b localhost:9092 -t activities -P  -l Static\ data/data.json
   # rm data.json data.zip # TODO: verify the data persists after killing the container
   
   


Running:
if the spark server started succesfully in the previous stage, you can now connect using http://localhost:8888 and open jupyter notebook

open  http://localhost:4040 to see details on stages, environment etc.

 or just run the script `run` that will start the service, and then open the browser for you.


Uninstalling:
linux/mac: 
```
  $ docker-compose down
  $ docker kill `docker ps`
  $ docker rm `docker ps -aq`
  $ docker rmi `docker images`
```
Now you can uninstall docker itself:
`sudo apt remove docker`
  
 
