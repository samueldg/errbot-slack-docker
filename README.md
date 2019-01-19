# Errbot Slack

[![Docker Build](https://img.shields.io/docker/build/samueldg/errbot-slack.svg)](https://hub.docker.com/r/samueldg/errbot-slack/builds/)

Run [Errbot](http://errbot.io/en/latest/) with a Slack backend, in Docker.

## Setup

First, set up the directory structure and grab the configuration template:

```sh
mkdir errbot
cd errbot/
mkdir data plugins
curl -o config.py http://errbot.io/en/latest/_downloads/config-template.py
```

The structure should look like this:

```
errbot
└─ data/       # Persisted data for the bot and plugins.
└─ plugins/    # Additional plugins installed.
└─ config.py   # Bot configuration file.
```

At this point, follow the instructions in `config.py` to configure the bot (for more info, refer to [Slack configuration](http://errbot.io/en/latest/user_guide/configuration/slack.html)):

```sh
vi config.py
```

You will need at least the following entries:

```python
BACKEND = 'Slack'
BOT_DATA_DIR = '/errbot/data'
BOT_EXTRA_PLUGIN_DIR = '/errbot/plugins'
BOT_IDENTITY = {'token': 'xoxb-SLACK-TOKEN-FOR-THE-BOT'}
CHATROOM_PRESENCE = ()
```

Then run the Docker container:

```sh
docker run \
    -d \
    --restart=always \
    --name errbot \
    -v "$PWD/data:/errbot/data" \
    -v "$PWD/plugins:/errbot/plugins" \
    -v "$PWD/config.py:/errbot/config.py" \
    samueldg/errbot-slack:latest
```
