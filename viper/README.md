# Viper - Binary Analysis and Management Framework

[Viper](https://viper.li/en/latest/) permits creating a repository of malicious samples as well as provides interfaces to well-known malware analysis applications and platforms.


To build the Docker image, please copy the Dockerfile to a new directory, and run 

```bash
$ cd <directory> && sudo docker build --tag=viper .
```


Viper can then be invoked with 

```bash
$ sudo docker run --rm -p <local port>:8080 viper
```

By default, the web interface of Viper is started and can be accessed via the selected local port at http://127.0.0.1.

The default login credentials are **admin:viper**.


If you would rather like to work with the terminal version, please run 

```bash
$ sudo docker run -it --rm viper bash
```

and then start Viper with the `viper-cli` command.

