# docker-node
Unofficial Alpine Linux nodejs containers


## Publish a new node runner container for a new node version

1. Edit the `5.7/alpine/Dockerfile` files to change the node version variable (`NODE_VERSION`)
2. Build a new image: `$ docker build -t rezzza/docker-node:latest 5.7/alpine`
3. Create the corresponding tag (replace the `z`): `$ docker tag latest rezzza/docker-node:5.7.z`
4. Push it! `$ docker push rezzza/docker-node`

## Publish a new VeryLastRoom image

1. Build a new image: `$ docker build -t rezzza/docker-node:web.client.vlr-latest vendor/web.client.vlr`
2. Push it! `$ docker push rezzza/docker-node`
