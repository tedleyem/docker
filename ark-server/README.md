# ARK Game Dedicated Server
ARK-server with arkmanager, configurable by environment-variables, upon a slim debian image

[Docker Image: hermsi/ark-server](https://hub.docker.com/r/hermsi/ark-server/)


### Ways to run
You may want to change SESSION_NAME, ADMIN_PASSWORD or host-volume
```bash
docker run -d --name="ark_server" --restart=always -v "${HOME}/ark-server:/app" -e SESSION_NAME="Awesome ARK is awesome" -e ADMIN_PASSWORD="FooB4r"
```

| Variable      | Default value     | Explanation |
| ------------- | ----------------- |------------ |
| SESSION_NAME  | Dockerized ARK Server by github.com/hermsi1337 | The name of your ARK-session which is visible in game when searching for servers |
| SERVER_MAP    | TheIsland | Desired map you want to play |
| SERVER_PASSWORD | YouShallNotPass | Server password which is required to join your session. (overwrite with empty string if you want to disable password authentication) |
| ADMIN_PASSWORD |Th155houldD3f1n3tlyB3Chang3d |Admin-password in order to access the admin console of ARK |
| MAX_PLAYERS | 20 | Maximum number of players to join your session |
| UPDATE_ON_START | false | Whether you want to update the ARK-server upon startup or not |
| BACKUP_ON_STOP | false | Create a backup before gracefully stopping the ARK-server |
| PRE_UPDATE_BACKUP | true | Create a backup before updating ARK-server |
| WARN_ON_STOP | true | Broadcast a warning upon graceful shutdown |
| ENABLE_CROSSPLAY | false | Enable crossplay. When enabled battleye should be disabled as it likes to disconnect epic players |
| DISABLE_BATTLEYE | false | Disable Battleye protection |
| ARK_SERVER_VOLUME | /app | Path where the server-files are stored |
| GAME_CLIENT_PORT | 7777 | Exposed game-client port |
| UDP_SOCKET_PORT | 7778 | Raw UDP socket port (always Game client port +1) |
| RCON_PORT	27020 | Exposed | RCON port |
| SERVER_LIST_PORT | 27015 | Exposed server-list port |
| GAME_MOD_IDS | empty | Additional game-mods you want to install, seperated by comma. (e.g. GAME_MOD_IDS="487516323,487516324,487516325") |


---
#### Tweak configuration

After your container is up and ARK is installed you can start tweaking your configuration.
Basically, you can modify every setting which ARK-Server-Tools are capable of.
For reference of the available commands check [their docs⁠](https://github.com/FezVrasta/ark-server-tools#configuration)


The main config files are located at the following path in the container:
```
    /app/server/ShooterGame/Saved/Config/LinuxServer/GameUserSettings.ini
    /app/server/ShooterGame/Saved/Config/LinuxServer/Game.ini
```
You can easily apply your changes directly into these files.

Alternatively, it is possible to run any available command with ARK-Server-Tools and apply your changes that way:
```
$ docker exec ark_server arkmanager status
$ docker exec ark_server arkmanager update --force
$ docker exec ark_server arkmanager installmods
```
For a full list of all available commands [check here⁠](https://github.com/FezVrasta/ark-server-tools#commands-acting-on-instances)


Add cronjobs

It is also possible to add cronjobs inside the cointainer. You could use the crontab for update- or backup-stuff.
In order to do so, edit the crontab-file located direct in the server-volume.
```
$ vim "${HOME}/ark-server/crontab"
```
Add your desired cronjobs with valid syntax:


Add your desired cronjobs with valid syntax:
```
0 0 * * * arkmanager update --warn --update-mods >> ${SERVER_VOLUME}/log/crontab.log 2>&1
0 0 * * * arkmanager backup >> ${SERVER_VOLUME}/log/crontab.log 2>&1
```
Close file (:wq) and restart the container:
```
$ docker restart ark_server
```
