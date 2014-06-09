Development environment provisioner using Docker and Vagrant!

Uses `config.yml` to create Docker containers as Vagrant **providers**. These containers will run in a proxy VM which is configured with a Vagrantfile in `dproxy`.

Configuring Services
================
git clone this repo:

`git clone https://github.com/jasonblanchard/docker-devbox2.git [project-name]`

Copy `config.yml.example` to `config.yml`:

`cp config.yml.example config.yml`

Each service in `config.yml` includes a `docker_config` which uses the same parameters as Vagrant Docker provider configuration: http://docs.vagrantup.com/v2/docker/configuration.html

See inline documentation in `config.yml.example` for more information

Usage
=====
Once the Docker containers are configured, follow the Vagrant Docker provider documentation for usage: http://docs.vagrantup.com/v2/docker/basics.html

Accessing the Docker Daemon
===========================
The proxy VM binds the Docker daemon to `0.0.0.0:4243` and exposes port 4243 to your host OS.

This means that you can attach `docker` commands on your host OS to the docker daemon running on the proxy VM. To do so, either tell docker the host to attach to:

`docker -H tcp://localhost:4243 [command]`

or put this line in your `bash_profile` to ser the the `DOCKER_HOST` environment variable:

`export DOCKER_HOST=tcp://localhost:4243`

Docker will honor this environment variable when you execute any `docker` commands.

More info on the Docker daemon here: http://docs.docker.io/reference/commandline/cli/#daemon

Known Issues
============
If you see this message when you first run `vagrant up`:

```
A Docker command executed by Vagrant didn't complete successfully!
The command run along with the output from the command is shown
below.

Command: "docker" "ps" "-a" "-q" "--no-trunc"

Stderr: 2014/06/09 20:55:18 Get http:///var/run/docker.sock/v1.12/containers/json?all=1: dial unix /var/run/docker.sock: permission denied
```

Just run `vagrant up` again.
