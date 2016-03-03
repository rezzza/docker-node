# docker-node
Unofficial Alpine Linux nodejs containers

## Publish a new node runner container for a new node version

1. Edit the `5.7/alpine/Dockerfile` file to change the node version variable (`NODE_VERSION`)
2. Build a new image:
```
$ docker build -t rezzza/docker-node:latest 5.7/alpine
```
3. Create the corresponding tag (replace the `z`):
```
$ docker tag latest rezzza/docker-node:5.7.z
```
4. Push it!
```
$ docker push rezzza/docker-node
```

## Upgrade node in the VeryLastRoom image

1. Edit the `vendor/web.client.vlr/Dockerfile` file to use the corresponding parent node image
2. Build a new image:
```shell
$ docker build -t rezzza/docker-node:web.client.vlr-latest vendor/web.client.vlr
```
3. Create the corresponding tag (adapt the image version and the node version):
```shell
$ docker tag *insert_the_image_id_here* rezzza/docker-node:web.client.vlr-1.y.z-node_x.y.z
```
4. Push it!
```shell
$ docker push rezzza/docker-node
```
