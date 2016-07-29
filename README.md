# VMWorld 2016 Demo
clone this project
`git clone https://github.com/ManoMarks/vmworld2016demo.git`

## Docker for Mac/Windows demo:
1. Edit index.html to change the title
2. Make sure you're in the project folder, the run
   `docker run --name vmworld -v `pwd`:/usr/share/nginx/html -d -p 8080:80 nginx`
3. Open browser to localhost:8080
4. click tweet button and follow directions
5. In terminal run 
    `$ docker stop vmworld`
    `$ docker rm vmworld` 



