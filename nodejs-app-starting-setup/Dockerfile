# we always start with FROM base image
FROM node 

WORKDIR /app

#which files that live in our local machine should go into the image
# Here you specify 2 paths, the first path is the local path where the files live that should be copied into the image
#And if you just specify a dot here(.) that basically tells docker that is in the same folder that contains the Dockerfile
#exluding the Dockerfile (i.e all the folders, subfolders and files that are here will be copied into the img)
#The second path is the path inside of the img. Every img has its own internal file system. we could use the root entry (.)
#but it's better that we create a folder in the root entry and call it whatever, in this case "/app":
COPY . /app
#COPY . ./
#Which is the same as COPY . ./

#now we need to thing about what we need to do outside of the container. In this case run npm install
#This commands will be rin in the working directory of our container. By default, the working directory is the root folder.
#Hoever we want to run those in the folder we created in which we pasted the code "/app".
#So we add WORKDIR /app in line 4
#And change line 12 for line 13, as now "." in the img will be the /app folder. We can keep using line 12 to use absolute paths
#that's also fine

RUN npm install

#Now we can think that we would "RUN node server.js" as we would do in the console
#But that's be incorrect. We want to have the code and the dependencies in the img, but we don't
#want to start a server if we don't start the container based on this img.
#That's why we will use CMD (stands for command), rather than RUN. CMD won't be executed when
#the img is created but when a container is started based on the img.
#This is the way of doing it with CMD: CMD ["node", "server.js"]
#However, we can't forget that our contained is isolated from our local environment.
#This node application listens to the port 80 (this is in the server.js code)
#So when you listen to the port 80 inside the container, the container does not export that port
#to out local machine, so we need to give docker the order to expose it:
#The expose instruction is optional, as the important thing is to add "-p local_port:docker_port" when running the img.
#We pass the environment variables, in this case is PORT with a default value of 80. we use an env variable for this:
ENV PORT 80

EXPOSE $PORT
#EXPOSE 80

#If we change the environmental variable, we do it when running the container:
#   docker run -p 3000:8000 --env PORT=8000
#or
#   docker run -p 3000:8000 -e PORT=8000
#for several:
#   docker run -p 3000:8000 -e PORT=8000 -e ANOTHER_VAR=699
#Or you can create a .env file and run it like:
#   docker run -p 3000:8000 --env-file ./.env #This means the file named".env" which is in this path, so "./"

CMD ["node","server.js"]

#then we need to run:
#         docker build .
# The dot(.) in the instruction is specifying the path where the dockerfile is. That dot means in the current folder.
#And then we run this to actually run it:
#         docker run -p 3000:80 [IMAGE]
# -p stands for publish. we're telling docker to publish its port 80 to out local port 3000.
#If we want to shut down the container we do:
# docker stop [container_name] 
#Reminder: to see the running containers: docker ps
#Reminder: to see the containers(including exited): docker ps -a