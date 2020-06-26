FROM node:12.13.0-alpine as builder

WORKDIR /app

COPY ./package.json ./.npmrc ./yarn.lock ./
RUN yarn
COPY . .
RUN yarn build:prod

USER node

CMD [ "node", "server.js"]