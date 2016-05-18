# rpi-alpine-ngrok
Raspberry Pi Docker image with minimal GNU/Linux system with Ngrok  

### Create a Dockerfile

```
FROM hypriot/rpi-alpine-scratch

RUN apk update && \
apk upgrade && \
apk add bash && \
apk add curl && \
rm -rf /var/cache/apk/*

ADD https://api.equinox.io/1/Applications/ap_pJSFC5wQYkAyI0FIVwKYs9h1hW/Updates/Asset/ngrok.zip?os=linux&arch=amd64&channel=stable /
RUN unzip ngrok.zip -d /bin && \
 rm -f ngrok.zip && \
 touch /.ngrok

CMD /bin/ngrok -config /.ngrok -log stdout $(netstat -nr | grep '^0\.0\.0\.0' | awk '{print $2}'):$HTTP_PORT
```

### Build image

`docker build -t alpine-ngrok`



