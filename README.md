# ASFbot

### Telegram Bot coded in python to control your ASF instance.
Control your ASF instance anywhere.

[![Docker Automated build](https://img.shields.io/docker/automated/dmcallejo/asfbot.svg)](https://hub.docker.com/r/dmcallejo/asfbot/) [![Docker Build Status](https://img.shields.io/docker/build/dmcallejo/asfbot.svg)](https://hub.docker.com/r/dmcallejo/asfbot/) [![Docker Pulls](https://img.shields.io/docker/pulls/dmcallejo/asfbot.svg)](https://hub.docker.com/r/dmcallejo/asfbot)

## Usage:
 - Executable: (python3) bot.py
 - Arguments:
   - ```--host``` : ASF IPC host (defaults to ```127.0.0.1```)
   - ```--port``` : ASF IPC listening port (defaults to ```1242```)
   - ```--token``` : Telegram API token given by @botfather (**mandatory**).
   - ```--alias``` : Telegram alias of the bot owner. Only this user can send commands to ASF. (**mandatory**).

Once the bot has started and verified the connection to the ASF instance, you can send commands through your telegram bot using standard ASF notation (i.e.: ```!status asf```) or Telegram notation (i.e.: ```/status asf```). 
The bot also reads messages containing Steam cd-keys. It will automatically parse every key and activate them on your accounts with ```!redeem asf {{parsed_cdkey}}``` notifying you the process.

## Quickstart (with docker)
1. Create a bot via [@botfather](t.me/BotFather).
2. Copy and fill the ```docker-compose.yml``` example below.
3. Start it!

## Notes
I recommend running it via its Docker image. Here it is an example docker-compose.yml to run bot ASF and the bot on Docker. Copy this to a file named ```docker-compose.yml```, fill the appropriate missing data:
 - (1) your ASF/config directory path
 - (2) Your Telegram bot token
 - (3) Your Telegram user alias

 Run ```docker-compose up -d```

P.S.: ARM docker images are untested. Did you try them? Contact me!

## docker-compose.yml template
```
version: '3.2'
asf:
  image: justarchi/archisteamfarm
  container_name: asf
  hostname: asf
  restart: unless-stopped
  environment:
    - ASF_ARGS=--server
  ports:
    - 1242:1242
  volumes:
    - # (1) paste here your old ASF/config directory :/app/config

asfbot:
  image: dmcallejo/asfbot
  container_name: asfbot
  hostname: asfbot
  restart: unless-stopped
  command: --host asf
  environment:
    - TELEGRAM_BOT_TOKEN= # (2) paste here your API token given by @botfather
    - TELEGRAM_USER_ALIAS= # (3) paste here your Telegram alias i.e.: @myalias
```
