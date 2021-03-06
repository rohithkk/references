# Docker Commands Quick Reference

### Common Syntax for running Docker commands

   `docker < command > <sub command> [options ]`


1. Get the Docker Client and Server version

    `docker version`
    
2. Start new container

    `docker container run --publish <port>:<port> <image_name>`
    
    **Example:**
       
     To start a new nginx container on port 80,
         
        docker container run --publish 80:80 nginx
        
3. Start new container in detached mode

    `docker container run --publish <port>:<port> --detach <image_name>`

4. Start an existing stopped container

   `docker container start `

5. List currently running containers

    `docker container ls`
    
    > `docker container ps` also emits the same output. This was the old syntax.
    
6. Stop Docker container

    `docker container stop <container id>`
    
    > We don't have to type the complete container id. Usually the first 3-4 digits would be good enough to uniquely identify the container that we wish to stop out of all the currently running ones.
    
    To stop all running containers at once, run the following command
    
    `docker container stop $(docker container ls -aq)`
    
7. Remove stoped container(s)

   Remove a single stopped container
   
    `docker container rm <container id>`
    
   Remove multiple stopped containers
   
    `docker container rm <container1 id> <container2 id>  <container3 id>`

   Remove all stopped containers at once, run the following command
    
    `docker container rm $(docker container ls -q)`

8. To remove all stopped containers, dangling images, unused networks,

   `docker system prune`
    
   `docker system prune -f` or `docker system prune --force` to skip the warning.
 

9. View logs from a container

    `docker container logs [options] <container id>`
    
    > Options:  -f                      follow the log output, 
    >            --tail < number >         show the last <number> lines from the logs
   
10. List processes from a container

      `docker container top <container id>`
      
11. Display detailed config information for a container

     `docker container inspect <container id>`
     
12. View real time performance metrics from a container

    `docker container stats [container id]`
    
    "container id" is optional. If not passed, then the comand will output the stats from all the running containers.
    
13. Getting into shell inside a container  
    
     **Option 1 - run the container iteratively**
     
     `docker container run **-it** <image name> <command to run>`
     
     > Example: docker container run -it nginx bash
     
     > The above command starts a new nginx container and immediately runs the bash command on the container. You will be able to execute other commands on the shell.

    > The container stops as soon as we exit from the shell. This is because we overwrote the default command in the Dockerfile of the nginx image to "bash" which is only valid for shell lifetime.
    
    
     **Option 2 - run the exec command on a running container**
     
     `docker container exec **-it** <image name> <command to run>`
     
     > Example: docker container exec -it mysql bash
     
     > The above command starts a new process on the currently running "mysql" container and executes the bash command on it.

    > The container will continue to run even after exiting from the shell. This is a key difference between Option 1 and Option 2.
    
