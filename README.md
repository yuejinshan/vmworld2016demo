# VMWorld 2016 Demo
clone this project
`git clone https://github.com/ManoMarks/vmworld2016demo.git`

## Docker for Mac/Windows demo:
1. Edit index.html to change the title

2. Make sure you're in the project folder, the run

   `docker run --name vmworld -v 'pwd':/usr/share/nginx/html -d -p 8080:80 nginx`

3. Open browser to localhost:8080

4. click tweet button and follow directions

5. In terminal run 

    ```
    $ docker stop vmworld
    $ docker rm vmworld
    ``` 

## Swarm Mode demo:
### Preparation
create the nodes and swarm by running `swarm-node.vbox-setup.sh` from this repo on each demo machine

find ip address of manager1 machine

```
$ docker-machine ssh manager1
docker@manager1:~$ docker pull manomarks/visualizer
docker@manager1:~$ docker run -it -d -p 8080:8080 -e HOST=IP_ADDRESS -v /var/run/docker.sock:/var/run/docker.sock manomarks/visualizer docker pull manomarks/visualizer
```

open browser to IP_ADDRESS:8080
open another terminal window or tab

### Demo
1. Explain that you have a swarm with three manager nodes and three worker nodes runnning locally, show the visualizer and also use docker to list the nodes

	`docker node ls`

2. Demo adding a service

	```
	docker@manager1:~$ docker service create --name web nginx:latest
	docker@manager1:~$ docker node ls
	```

3. Switch over to the browser and show them the node with one service one it

4. Show them scaling up the service

	`docker@manager1:~$ docker service scale web=15`

5. Switch back to the browser and show them how the service grows

6. In the command windows set one of the nodes to drain mode, this will force the containers to reschedule onto the other machines. 

	`docker@manager1:~$ docker node update --availability drain worker1`
	
7. Show the redistributed containers in the visualizer, and show that the availability of `worker1` is set to drain (the visualizer will still show `worker1` as green because it is still running)

	`docker@manager1:~$ docker node ls worker1 --pretty` 
	
8. Scale the web service down to 10 and show how all the containers now have 2 tasks on them

	`docker@manager1:~$ docker service scale web=10`
	
9. Bring `worker1` back online and show it's new availability

	`docker node update --availability active worker1`
	
	`docker node inspect worker1 --pretty`
	
10. Scale it back up to 12 and use the command line to show how many replicas are running

	`docker service scale web=12`
	
	`docker service ls`
	
	`docker service inspect web --pretty`

11. when they are done, remove the service

	`docker@manager1:~$ docker service remove web`

### Cleanup at end of conference
Clean up the machine by running `swarm-node-vbox-teardown.sh`  
