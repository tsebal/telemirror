# Telegram channel mirroring app 

App helps make telegram channel mirror. We will use Telegram client API because Bot API have limited functionality. 

### Functionality
1. Catching *NewMessage* event and sending them forward
2. Flexible source and target channels mapping

## Prepare
1. [Create Telegram App](https://my.telegram.org/apps)
2. Obtain API App ID and hash
![Telegram API Credentials](/images/telegramapp.png)
3. Setup Postgres database
4. Fill [.env-example](.env-example) with your data and rename it to .env 
    1. SESSION_STRING can be obtained by running [login.py](login.py) with putted API_ID and API_HASH before.

```bash
API_ID=test # Telegram app ID
API_HASH=test # Telegram app hash
SESSION_STRING=test # Telegram session string
# Mapping between source and target channels
# Channel id can be fetched by using @messageinformationsbot telegram bot
# and it always starts with -100 prefix
# [id1, id2, id3:id4] means send messages from id1, id2, id3 to id4
# id5:id6 means send messages from id5 to id6
# [id1, id2, id3:id4];[id5:id6] semicolon means AND
CHAT_MAPPING=[-100999999,-100999999,-100999999:-1009999999];
TIMEOUT_MIRRORING=0.1 # Delay in sec between sending or editing messages
REMOVE_URLS=false   # Apply removing URLs on messages
# Remove URLs whitelist
REMOVE_URLS_WL=youtube.com,youtu.be,vk.com,twitch.tv,instagram.com

## Deploy
### Locally
1. Create and activate python virtual environment
```bash
python -m venv myvenv
source myvenv/Scripts/activate # linux
myvenv/Scripts/activate # windows
```
2. Install depencies
```bash
pip install -r requirements.txt
```
3. Run
```bash
python app/telemirror.py
```

## Heroku
[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/tsebal/telemirror)

or

1. Clone project
```
    git clone https://github.com/tsebal/telemirror.git
```
2. Create new heroku app within Heroku CLI
```
    heroku create {your app name}
```
3. Add heroku remote
```
    heroku git:remote -a {your app name}
```
4. Set environment variables to your heroku app from .env by running .bash script
```
    ./.bash
```

5. Upload on heroku host
```
    git push heroku master
```

6. Start heroku app
```
    heroku ps:scale run=1
```

### original https://github.com/khoben/telemirror