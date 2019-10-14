FROM node:10.16-stretch

ARG DEBIAN_FRONTEND=noninteractive

RUN npm install -g @vue/cli \
  && vue -V

WORKDIR /app

EXPOSE 8080
