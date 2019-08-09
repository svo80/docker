# Docker Images

This repository contains *Dockerfiles* for building images of utilities and frameworks used in the malware analysis area.

To build an image, please copy the respective Dockerfile in a new directory, and run

```bash
$ cd <directory> && sudo docker build --tag=<image name> .
```

To start a utility in a container, please run

```bash
$ sudo docker run --rm -p <local port>:<remote port> <image name>
```

If you would like to inspect the contents of a container or require terminal access, please run

```bash
$ sudo docker run -it --rm -p <local port>:<remote port> <image name> bash
```

## Available Dockerfiles  

* **Viper** 

[Viper](https://viper.li/en/latest/) permits creating a repository of malicious samples as well as provides interfaces to well-known malware analysis applications and platforms.


