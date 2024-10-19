# Docker-Nagios

Docker image for Nagios

Nagios Core 4.4.5 running on Ubuntu 16.04 LTS with NagiosGraph & NRPE

### Running
Run with the example configuration with the following:

```sh
docker run -d --privileged --name nagios -v /:/overlay/opt -p 80:80 -p 5666:5666 tmeralus/nagios:latest
```
roles/ansible-role-nagios-docker/configs/objects/
#### Credentials

The default credentials for the web interface is `nagiosadmin` / `nagios`

### Configurations
More configuraion settings can be found [here](configs.md)
