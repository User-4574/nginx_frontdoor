FROM nginx:latest
ENV DOCKERIZE_VERSION v0.6.1

RUN apt-get update\
	&& apt-get install -y --no-install-recommends procps iputils-ping cron python3-certbot-dns-google wget vim\
	&& apt-get clean -y \
	&& rm -rf /var/lib/apt/lists/* \
	&& wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
  	&& tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
   	&& rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
	&& mkdir /templates \
	&& mkdir /scripts
COPY scripts/* /scripts/
COPY templates/* /templates/
#Fixup VIm
RUN echo "set mouse-=a">>/root/.vimrc
RUN echo "syntax on">>/root/.vimrc
CMD ["/scripts/start"]


