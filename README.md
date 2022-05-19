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

## 2. Publish the image to GitHub Container Registry using a GitHub Action

To publish a Docker image to GitHub Container I need to have a personal access token. Follow [this](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) guide for more information.

Then go to repsitory settings and add that token as a secret (Secret name is `GHCR_TOKEN`). If you don't know about GitHub secrets please go through [this](https://docs.github.com/en/actions/security-guides/encrypted-secrets) guide.

