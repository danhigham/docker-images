FROM node:lts-alpine

RUN apk update 
RUN apk add python3 py3-pip g++ make linux-headers bash

ENV NPM_CONFIG_PREFIX=/home/node/.npm-global

USER node
RUN npm install -g cncjs

EXPOSE 8000
ENTRYPOINT ["/home/node/.npm-global/bin/cncjs"]