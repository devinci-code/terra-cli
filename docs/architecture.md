Terra Architecture
====================

Here are the hows and whys of terra's architecture.

### boot2docker
Since docker runs different containers using the same linux kernal. The containers must be in a linux environment. OSX runs on top of BSD, not linux, so it requires the docker deamon run on inside a VM that does have linux. That's where boot2docker comes in as it's basically a small linux VM with a docker daemon already setup. Terra doesn't care where the boot2docker VM is, and you could roll your own VM instead of boot2docker if you really wanted to, but terra (and the docker commands it runs on your behalf) do need to know the hostname/ip address that the docker daemon is listening on. Most of the time that is 192.168.10.10. (I think) terra looks at your bash environment variable DOCKER_HOST to know which to use by default.

### docker-compose.yml
Most of what Terra is doing when you create an environment is creating a custom docker-compost.yml file for you. Normally when using docker-compose directly, you would create a docker-compose.yml file in the root of your repo and then call `docker-compose up -d` to spin up all the containers. With terra, you instead define some settings in a .terra.yml file of your repo and terra generates the docker-compose.yml file based on it's intial template and what you put in .terra.yml. It then places that file in something like vim `~/.terra/environments/drupal7/drupal7-local/docker-compose.yml` and runs `docker-compose -f` so the docker-compose file doesn't need to be in the same place as repo.

### Apps
What terra currently calls "Apps" are really just a repo url (can be anywhere, github, acquia, custom) and a name for that repo. Creating an app doesn't actually do much of anything but store that information inside of ~/.terra/apps

### Environments
Environments are an instantiation of an App. When you add an Environment to an App, it just means that the repo is checked out, the docker-compose.yml file is generated, and docker-compose up is run.


