FROM golang:1.17 AS builder

ARG APP_DIR=/app

WORKDIR ${APP_DIR}

ADD main.go .
ADD go.mod .
ADD go.sum .

# /app/main
RUN go build -o main main.go

FROM golang:1.17 

ARG APP_DIR=/app

WORKDIR ${APP_DIR}

COPY --from=builder ${APP_DIR}/main .
ADD public public
ADD templates templates

ENV APP_PORT=3000 INSTANCE_NAME="dov-go-bear"

EXPOSE ${APP_PORT}

ENTRYPOINT [ "./main" ]