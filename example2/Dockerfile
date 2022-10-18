FROM node:14.20.1-alpine3.16 AS build

RUN apk update \
    && apk add --no-cache wget zip \
    && mkdir -p /app \
    && wget -O develop.zip "https://github.com/LaBelleAssiette/UC_FRONT_2022/archive/refs/heads/develop.zip"

RUN unzip develop.zip -d /tmp \
    && mv /tmp/UC_FRONT_2022-develop/* /app \ 
    && ls -l

WORKDIR /app
RUN yarn install \
    && yarn build

FROM nginx:1.21.6-alpine AS front

COPY --from=build /app/build /var/www/html
COPY default.conf /etc/nginx/conf.d/default.conf