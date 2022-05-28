FROM alpine:latest
ENV PROXY2_VERSION v7.2.1
ENV	DOCKERIZE_VERSION v0.6.1

RUN apk add --no-cache wget bash \
	&& wget https://github.com/oauth2-proxy/oauth2-proxy/releases/download/$PROXY2_VERSION/oauth2-proxy-$PROXY2_VERSION.linux-amd64.tar.gz \
	&& mkdir /oauth2-proxy \
  	&& tar -C /oauth2-proxy -xzvf oauth2-proxy-$PROXY2_VERSION.linux-amd64.tar.gz \
   	&& rm oauth2-proxy-$PROXY2_VERSION.linux-amd64.tar.gz \
	&& mv /oauth2-proxy/oauth2-proxy-$PROXY2_VERSION.linux-amd64/oauth2-proxy /oauth2-proxy/ \
	&& rmdir /oauth2-proxy/oauth2-proxy-$PROXY2_VERSION.linux-amd64 \
    && wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
	&& mkdir /scripts
COPY scripts/* /scripts/
COPY templates/* /templates/
#Fixup VIm
RUN echo "set mouse-=a">>/root/.vimrc
RUN echo "syntax on">>/root/.vimrc
CMD ["/scripts/start"]


