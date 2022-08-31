Use the instructions here to run your own local (on your Window/Mac/Linux) machine.

Steps:
1. install docker  or docker desktop
1.1 install docker-compose: `sudo apt install docker-compose`
2. run the command: docker-compose up -d
3. import some data into the kafka server now running in your machine.
   unzip static_data.zip
   sudo apt install kafkacat
   kafkacat -b localhost:9093 -t activities -P  -l data.json
   rm data.json data.zip # TODO: verify the data persists after killing the container
   
   


Running:
if the spark server started succesfully in the previous stage, you can now connect using http://localhost:8888 and open jupyter notebook

open  http://localhost:4040 to see details on stages, environment etc.


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
  
 
