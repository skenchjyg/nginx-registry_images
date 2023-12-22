FROM alpine

RUN apk add --update apache2-utils \
    && rm -rf /var/cache/apk/*

RUN mkdir /auth
ENTRYPOINT ["htpasswd", "-Bbn", "registry.password adminuser", ">", "/auth/registry.password"]
