Terra Architecture
====================

Here are the hows and whys of terra's architecture.

### boot2docker
Since docker runs different containers using the same linux kernal. The containers must be in a linux environment. OSX runs on top of BSD, not linux, so it requires the docker deamon run on inside a VM that does have linux. That's where boot2docker comes in as it's basically a small linux VM with a docker daemon already setup. Terra doesn't care where the boot2docker VM is, and you could roll your own VM instead of boot2docker if you really wanted to, but terra (and the docker commands it runs on your behalf) do need to know the hostname/ip address that the docker daemon is listening on. Most of the time that is 192.168.10.10. (I think) terra looks at your bash environment variable DOCKER_HOST to know which to use by default.

### docker-compose.yml
Most of what Terra is doing when you create an environment is creating a custom docker-compost.yml file for you. Normally when using docker-compose directly, you would create a docker-compose.yml file in the root of your repo and then call `docker-compose up -d` to spin up all the containers. With terra, you instead define some settings in a .terra file of your repo and terra creates the docker-comp
