FROM node:12.13.0-alpine as builder

WORKDIR /app

COPY ./package.json ./.npmrc ./yarn.lock ./
RUN yarn
COPY . .
RUN yarn build:prod

FROM node:12.13.0-alpine

WORKDIR /usr/src/app

ENV NODE_ENV production
COPY --from=builder /app/node_modules  ./node_modules
COPY --from=builder /app/build  .
COPY --from=builder /app/.env  ./.env
COPY --from=builder /app/newrelic.js .
COPY --from=builder /app/upload-source-map.js .
COPY --from=builder /app/sentry-client.properties .
COPY --from=builder /app/sentry-server.properties .
COPY --from=builder /app/.npmrc .

RUN yarn global add pm2@4.4.0

USER node

CMD [ "pm2", "start", "server.js", "-i", "0", "--no-daemon"]