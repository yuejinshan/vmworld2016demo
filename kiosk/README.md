# VMworld 2016 Kiosk Demo

## Demo setup
1. Ensure the laptop has Docker for Mac or Docker for Windows installed

## Docker for Mac/Windows demo:

2. To launch the container type the following command in the terminal window

   `docker run --name vmworld -d -p 8080:80 mikegcoleman/vmworld2016`

3. Switch to a web browser and navigate to: `http://localhost:8080`

4. Click Tweet button and follow the directions (don't worry, we don't save the Tweet credentials, since we'll destroy the container in the next step)

5. Switch back to the terminal and execute the following to commands to stop the container, and then remove it.  

    ```
    $ docker stop vmworld
    $ docker rm vmworld
    ``` 

