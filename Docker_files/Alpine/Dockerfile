FROM alpine:3.10

ENV MONGO_URL=mongodb://mongodb:27017/tdarr
ENV PORT=8265
ENV ROOT_URL=http://0.0.0.0/
ENV NODE_ARGS="--max-old-space-size=16384"

RUN \
  apk add --no-cache \
        git \
        exiftool \
	nodejs \
	unzip && \
  apk add --no-cache --repository="http://dl-cdn.alpinelinux.org/alpine/edge/testing" \
    ffmpeg \
    handbrake \
    handbrake-gtk

ADD Tdarr /app/Tdarr

RUN export uid=1000 gid=1000 && \
    mkdir -p /home/Tdarr && \
    mkdir -p /home/Tdarr/media && \
    mkdir -p /temp && \	
    echo "Tdarr:x:${uid}:${gid}:Tdarr,,,:/home/Tdarr:/bin/bash" >> /etc/passwd && \
    echo "Tdarr:x:${uid}:" >> /etc/group && \
    chown ${uid}:${gid} -R /home/Tdarr && \
    chown ${uid}:${gid} -R /temp && \
    chown ${uid}:${gid} -R /app/Tdarr/bundle/programs/server/assets/app

USER Tdarr    
ENV HOME /home/Tdarr

RUN cp /usr/bin/ffmpeg /app/Tdarr/bundle/programs/server/assets/app/ffmpeg/ffmpeg42/ffmpeg

EXPOSE 8265
WORKDIR /app/Tdarr/bundle
CMD ["node","--max-old-space-size=16384","main.js"] 
