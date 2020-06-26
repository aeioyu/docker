FROM node:12.13.0-alpine as builder

WORKDIR /app

COPY ./package.json ./.npmrc ./yarn.lock ./
RUN yarn
RUN yarn global add pm2@4.4.0

COPY . .
RUN yarn build:prod

USER node

CMD [ "pm2", "start", "server.js", "-i", "0", "--no-daemon"]