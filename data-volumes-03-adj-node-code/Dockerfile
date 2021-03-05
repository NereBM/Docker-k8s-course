FROM node:14

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 80

#in volume, we add a folder inside our container, but this will give as an anonymous volume
#that won't persist when our container is shut down. So we remove the instruction
#since we'll create a named volume
#VOLUME ["/app/feedback"]
#to create a named volume, we run this:
#  docker run -d -p 3000:80 --rm --name feedback-app -v feedback:/app/feedback feedback-node:volumes
#this will mean:
#       -d "run in detatched mode"
#       -p 3000:80 "listen to port 80 of the container and link it to port 3000 in the local machine"
#       --rm "remove the container when stopped"
#       --name feedback-app "call the created app 'feedback-app' "
#       -v feedback:/app/feedback "create a named volume called 'feedback' in my local machine that is 
#           mapped to the container files system path /app/feedback which you want to save"
#       feedback-node:volumes "specifies the name(and tag) of the image that we want to build the container from"
#Instead of this, that would create a anonymous volume (that would dissapear when the container is stopped):
#  docker run -d -p 3000:80 --rm --name feedback-app feedback-node:volumes
#we can see our volume even after shutting down the container, running this command:
# docker volume ls

CMD [ "node", "server.js" ]