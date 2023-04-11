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