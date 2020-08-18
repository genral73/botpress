# botpress
The Conversational Platform with built-in language understanding (NLU), beautiful graphical interface and Dialog Manager (DM). Easily create chatbots and AI-based virtual assistants.


## Deploy using Binaries and link it with postgresql

1- You can download the binaries [here](https://s3.amazonaws.com/botpress-binaries):
```bash
cd /opt
wget https://s3.amazonaws.com/botpress-binaries/botpress-v12_10_5-linux-x64.zip
```

2- Extract the botpress file:
```bash
unzip botpress-v12_10_5-linux-x64.zip -d /opt/botpress
```

3- create the botpress role and database:
```bash
sudo su postgres
createuser -s -P botpressUser
createdb DB_botpress -O botpressUser
exit
```

4- Prepare the botpress as daemon
```bash
sudo vim /etc/systemd/system/botpress.service
"""
[Unit]
Description=botpess service
After=network.target postgresql.service

[Service]
Type=simple
Environment="PORT=3000"
Environment="DATABASE_URL=postgres://botpressUser:PWDbotpress@127.0.0.1:5432/DB_botpress"
Environment="BP_HOST=192.168.10.100"
Environment="EXTERNAL_URL=http://192.168.10.100:3000"
Environment="BP_PRODUCTION=true"
Environment="APP_DATA_PATH=/opt/botpress"
User=developer
ExecStart=/opt/botpress/bp

[Install]
WantedBy=multi-user.target
"""

sudo systemctl daemon-reload
sudo systemctl restart botpress.service 
```
5- Go to the admin panel on browser:
You can click [here http://192.168.10.100:3000](http://192.168.10.100:3000)
