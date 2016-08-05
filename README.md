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

    ```bash
    $ docker stop vmworld
    $ docker rm vmworld``` 

## Swarm Mode demo:
### Preparation
create the nodes and swarm by running `swarm-node.vbox-setup.sh` from this repo on each demo machine

find ip address of manager1 machine

```bash
$ docker-machine ssh manager1
docker@manager1:~$ docker pull manomarks/visualizer
docker@manager1:~$ docker run -it -d -p 8080:8080 -e HOST=IP_ADDRESS -v /var/run/docker.sock:/var/run/docker.sock manomarks/visualizer docker pull manomarks/visualizer```

open browser to IP_ADDRESS:8080
open another terminal window or tab

### Demo
1. Explain that you have a swarm with three manager nodes and three worker nodes runnning locally

2. Demo adding a service

```bash
docker@manager1:~$ docker service create --name web nginx:latest
docker@manager1:~$ docker node ls```

3. Switch over to the browser and show them the node with one service one it

4. Show them scaling up the service

`docker@manager1:~$ docker scale web=15`

5. switch back to the browser and show them how the service grows
6. when they are done, remove the service

`docker@manager1:~$ docker service remove web`

### Cleanup at end of conference
Clean up the machine by running `swarm-node-vbox-teardown.sh`  
