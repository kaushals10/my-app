#Web-browser doesn't understand JSX code.
#Tools like babble/webpack are used to transpile(convert) JSX code into plain JS code, which browsers can understand.
#FROM is a keyword in Dockerfile, it starts a <<BUILD STAGE>> of the Dockerfile 
FROM node:alpine3.18 as myalias

#Specifying directory where all the subsequent commands will be executed
WORKDIR /app

#Copy package.json from the location where Dockerfile is located into /app directory.
COPY package.json .

#Execute below command inside "/app" directory to download all dependencies specified in package.json file
RUN npm install

#Copy all contents from the location where Dockerfile is located into /app directory.
COPY . .

#Build the project
RUN npm run build

########################################################
########################################################
########################################################


#nginx is a web server
#1.23 is version of the web server 
#alpine indicates it is based on alpine linux
FROM nginx:1.23-alpine
WORKDIR /usr/share/nginx/html

#delete all the files from container's current directory 
RUN rm -rf *

#copy all the contents from the previous build stage into current working directory.
COPY --from=myalias /app/build .

#run nginx server in port 80
EXPOSE 80

#set nginx process as the main process and make sure it is running in foreground, 
#otherwise docker daemon thread will consider the container has terminated.
ENTRYPOINT ["nginx", "-g", "daemon off;"]