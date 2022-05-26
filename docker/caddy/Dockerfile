FROM caddy:2.5.1-builder-alpine

RUN xcaddy build --with github.com/darkweak/souin/plugins/caddy@latest

# See https://caddyserver.com/docs/conventions#file-locations for details
ENV XDG_CONFIG_HOME /config
ENV XDG_DATA_HOME /data

VOLUME /config
VOLUME /data

EXPOSE 80
EXPOSE 443
EXPOSE 2019

WORKDIR /srv
