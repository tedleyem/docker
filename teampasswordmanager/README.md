# Team Password Manager docker-compose stack
# Team Password Manager v.7.118.217 Docker Compose file
# More information: https://teampasswordmanager.com/docs/docker/


[How to create a full Team Password Manager installation with Docker Compose](https://teampasswordmanager.com/docs/docker-compose/)

[Team Password Manager](http://teampasswordmanager.com/ "Team Password Manager Homepage") is a web based password manager for teams. This repository aims to provide a basis to use teampasswordmanager in production via docker and docker-compose.
It features:
* almost completely automated setup of teampasswordmanager, only one config file needs to be touched
* builtin letsencrypt support: Helper script to test setup and obtain certificates via certbot
* automatic letsencrypt certificate renewal
* SSL offloading via a nginx reverse proxy
* OWASP recommended nginx settings

## Requirements ##

* docker >= 1.10
* docker-compose >= 1.8
* for LetsEncrypt: A domain pointing to the public IP address of the server intended to run the docker-compose stack for passbolt
* a server publicly reachable on ports 80 and 443

## How to use / Setup ##
1. Clone this repository
    ```bash
    git clone https://github.com/<user>/team-password-manager-dockere.git
    ```

2. Make sure you have docker and docker-compose up and running

3. Open .env with your favored editor and change the values to your needs

4. Execute the Team Password Manager installer
 To conclude the installation of Team Password Manager. You should execute the Team Password Manager installer.
 To do this: Open your browser and go to http://localhost/index.php/install
