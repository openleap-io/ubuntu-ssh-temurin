# SSH-Enabled Ubuntu Docker Image

[![Docker Image CI](https://github.com/openleap-io/ubuntu-ssh-temurin/actions/workflows/ci.yml/badge.svg)](https://github.com/openleap-io/ubuntu-ssh-temurin/actions/workflows/ci.yml)
[![Docker Image Deployment](https://github.com/openleap-io/ubuntu-ssh-temurin/actions/workflows/cd.yml/badge.svg)](https://github.com/openleap-io/ubuntu-ssh-temuring/actions/workflows/cd.yml)
[![Docker Pulls](https://img.shields.io/docker/pulls/openleap/ubuntu-ssh-temurin.svg)](https://hub.docker.com/r/openleap/ubuntu-ssh-temurin)
[![Maintenance](https://img.shields.io/badge/Maintained-Yes-green.svg)](https://github.com/openleap-io/ubuntu-ssh-temurin)

This Docker image provides an Ubuntu 24.04 base with SSH server enabled, maven and temurin 21 jdk installed. 
It allows you to easily create SSH-accessible containers via SSH keys or with a default username and password.
As versatile container it can be used as gitlab ci/cd executer image for maven builds and Dockerhub deploys. 

## Usage

### Cloning the Repository

To get started, clone the GitHub  [repository](https://github.com/openleap-io/ubuntu-ssh-temurin) containing the Dockerfile and scripts:

```bash
git clone https://github.com/openleap-io/ubuntu-ssh-temurin
cd ubuntu-sshd
```

### Building the Docker Image

Build the Docker image from within the cloned repository directory:

```bash
docker build -t my-ubuntu-ssh-temurin:latest .
```

### Running a Container

To run a container based on the image, use the following command:

```bash
docker run -d -p host-port:22 -e SSH_USERNAME=myuser -e PASSWORD=mysecretpassword -e AUTHORIZED_KEYS="$(cat path/to/authorized_keys_file)" my-ubuntu-ssh-temurin:latest
```

- `-d` runs the container in detached mode.
- `-p host-port:22` maps a host port to port 22 in the container. Replace `host-port` with your desired port.
- `-e SSH_USERNAME=myuser` sets the SSH username in the container. Replace `myuser` with your desired username.
- `-e PASSWORD=mysecretpassword` sets the SSH user's password in the container. Replace `mysecretpassword` with your desired password.
- `-e AUTHORIZED_KEYS="$(cat path/to/authorized_keys_file)"` sets authorized SSH keys in the container. Replace `path/to/authorized_keys_file` with the path to your authorized_keys file.
- `my-ubuntu-sshd:latest` should be replaced with your Docker image's name and tag.

### SSH Access

Once the container is running, you can SSH into it using the following command:

```bash
ssh -p host-port myuser@localhost
```

- `host-port` should match the port you specified when running the container.
- Use the provided password or SSH key for authentication, depending on your configuration.

### Note

- If the `AUTHORIZED_KEYS` environment variable is empty when starting the container, it will still launch the SSH server, but no authorized keys will be configured. You have to mount your own authorized keys file or manually configure the keys in the container.

## License

This Docker image is provided under the [MIT License](LICENSE).
