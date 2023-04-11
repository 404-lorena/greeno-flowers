# Greeno Flowers

An Node/Express Web Application serving up a static html landing page

## Goal: Build a docker image
1. Create a file named Dockerfile (capital D, no extension) in the root of the project. 
2. Add Docker commands:
```
FROM node:18
COPY . /app
WORKDIR /app
RUN npm install
CMD [ "npm", "start" ]
```

### Breakdown of commands
- The first path `FROM: node 18` is the path outside the image (the files that we should copy in). We're telling docker to use everything from this current directory. Basically, the “base image” to start from.  In this case, we’ll use the latest LTS version: `node:18`
- The second path `COPY: ./app` is inside the image (where the files should be stored. Detached from your own file system). The `COPY:` command tells Docker where to find source files and where to put them in the image.
- The `WORKDIR` specifies the working directory.  A little like `cd` in unix, `WORKDIR` changes the directory.  Since we copied everything into this directory, this is now the “root” of our project.
- `RUN:` Create a RUN command that should run while your image build. RUN runs a command (while building the image). In our case, we want to tell docker to install npm packages.
- `CMD`: Unlike RUN, CMD runs a command after the image is built, once we run the container. As with this project, CMD is typically a start command.


## Run Image in Container
1. When we built our image, we tagged it with a name.  Run this to list our available images.
```
docker images
```

2.  The `docker images` command shows the list of images we have built recently, and ours should be the most recent image built. We can run it using the `IMAGE ID` listed, or the `REPOSITORY` name
```
docker run greeno
```

NOTE: You’ll know it worked when you get the output from our application: "Server is listening at http://localhost:3000"

3. Vist http://localhost:3000. The site isn’t there! This is because we haven’t exposed a port. Back in the `Dockerfile` we should add an `EXPOSE` command right before `CMD`. This opens the port for our image.
```
EXPOSE 3000
```

4. However, this isn’t enough. When we run our image in a container (via the command line), we’ll have to publish the port:
```
docker run -p 3000:3000 greeno
```

NOTE: If all was done correctly, we should be able to see our beautiful flower site at http://localhost:3000
 

