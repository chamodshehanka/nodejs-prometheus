# Nodejs Prometheus
I gonna setup prometheus to monitor my nodejs app.

But first I need to contact the nodejs app and push docker image to container registry. 
Since I'm more familiar with GitHub Container Registry I'll push the image to my personal registry and I gonna use a GitHub action for that.

## 1. Containerize the app
In the root of the app folder I've create a Dockerfile and following instructions.
```bash
FROM node:alpine3.11

RUN mkdir /app

WORKDIR /app

COPY . . 

RUN npm install

EXPOSE 3000

CMD ["npm", "run", "start"]
```
also I have used `.dockerignore` to which I don't want to containerize with the app such as `node_modules` and `k8s` folders.

If I locally building the image I should use following commands to build the image and run the container.
#### Build Docker image
```shell
docker build -t {DOCKER_PROFILE_USERNAME}/node-app:latest .
```


#### Run a Docker container
```shell
docker run -p 3000:3000 chamodshehanka/node-app
```
