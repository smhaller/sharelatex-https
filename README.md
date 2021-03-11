## Configuration 
adapt the .env file and docker-compose to your configuration/settings.

## Installation, Usage and Inital startup

Install the docker engine: https://docs.docker.com/engine/install/

Install docker-compose:

(if you need pip: apt install python3-pip)

```
pip install docker-compose
```


use the command 
```
make
```
to generate the sharelatex-https docker image.



use the command
```
docker network create web
```
to create a network for the docker instances.

Then start docker containers (with loadbalancer):
``` 
export NUMINSTANCES=1
docker-compose up -d --scale sharelatex=$NUMINSTANCES
```



