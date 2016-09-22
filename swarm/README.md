# VMworld 2016 Demo

## Daily Demo setup
1. Make sure the laptop has the latest Docker Machine installed

1. Clone this project (if it doesn't exist)

	`git clone https://github.com/ManoMarks/vmworld2016demo.git`


1. Change into the `VMworld2016demo/swarm` directory (exact location depends on where you cloned the repo to) 

1. Execute `sh ./swarm-node-vbox-setup.sh` to build the Swarm cluster

1. Execute `docker-machine ls` and note the IP address of Manager1 and substitute it for `MANGER1_IP_ADDRESS` in the next 2 steps 

1. SSH into Manger1 and fire up the visualizer

	```
	$ docker-machine ssh manager1
	docker@manager1:~$ docker pull manomarks/visualizer
	docker@manager1:~$ docker run -it -d -p 8080:8080 -e HOST=MANGER1_IP_ADDRESS -v /var/run/docker.sock:/var/run/docker.sock manomarks/visualizer 
```

1. Open browser to `http://MANGER1_IP_ADDRESS:8080`


## Swarm Mode Demo
**Note**: Make sure you execute the following commands from the SSH session on Manager1

1. Explain that you have a swarm with three manager nodes and three worker nodes runnning locally, show the visualizer and also use docker to list the nodes

	`docker@manager1:~$ docker node ls`

2. Demo adding a service

	```
	docker@manager1:~$ docker service create --name web nginx:latest
	docker@manager1:~$ docker node ls
	```

3. Switch over to the browser and show the node with one service one it

4. Move back to the terminal window, and show scaling up the service

	`docker@manager1:~$ docker service scale web=15`

5. Switch back to the browser and show how the additional tasks running

6. In the command windows set one of the nodes to drain mode, this will force the containers to reschedule onto the other machines. 

	**Note**: Pick a node that has 1 or 2 tasks on it, we only use worker1 below as an example

	`docker@manager1:~$ docker node update --availability drain worker1`
	
7. Show the redistributed containers in the visualizer (the visualizer will still show `worker1` as green because it is still running)

	`docker@manager1:~$ docker node inspect worker1 --pretty` 
	
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

## Cleanup at end of the day
1. Clean up the machine by running `swarm-node-vbox-teardown.sh`  
