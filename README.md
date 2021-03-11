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
to generate the ldap-overleaf-ls docker image.




Then start docker containers:
``` 
docker-compose up -d
```

*Known Issue:*
During the first startup the certbot image will get an initial certificate - if that 
happens not in a very timely manner sharelatex will fail to start (due to the missing certificates 
nginx crashes). Solution: wait 10 seconds and restart the sharelatex container.

```
docker stop shrelatex-https
docker-compose up -d
```


