ARG NODE_VER=17

FROM node:${NODE_VER}

# build stage
ARG APP_DIR=/app

# cd in APP_DIR
WORKDIR ${APP_DIR}

ADD package.json .
ADD package-lock.json .
RUN npm ci

ADD main.js .
ADD public public
ADD views views

# copy files from host into container
#ADD . .

# run
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3  \
    CMD curl -s -f http://localhost:${APP_PORT} || exit 1

ENV APP_PORT=5000

EXPOSE ${APP_PORT}

ENTRYPOINT [ "node", "main.js" ]