FROM node:12

# define the working directory for the container during the build process
WORKDIR /usr/src/app

# copy the package.json from the current directory into the workdir for the build process
COPY package.json ./

# exec the installation process running a 'npm' command inside of the container
RUN npm install

# bundle app source
COPY . .

# define the port that the container will expose for the running application
EXPOSE 8080

# exec the command that will run the application
CMD [ "node", "server.js" ]
