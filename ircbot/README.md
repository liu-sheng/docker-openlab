##  OpenLab IRC Bot docker file

To persistent data, you may need to mount a docker volume

```bash
docker volume create --driver local --opt type=none \
    --opt device=/var/lib/openlab-ircbot \
    --opt o=bind openlab_vol
docker run -d --name openlab-ircbot \
    --mount type=volume,source=openlab_vol,target=/home/supybot \
    -e SUPYBOT_PASSWORD=youpassword \
    liusheng2048/supybot:latest
```
