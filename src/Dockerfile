FROM golang:1.15-alpine as dev-env

WORKDIR /app

FROM dev-env as build-env
COPY go.mod go.sum /app/
RUN go mod download

COPY . /app/

RUN CGO_ENABLED=0 go build -o /annotating-webhook

FROM alpine:3.10 as runtime

COPY --from=build-env /annotating-webhook /usr/local/bin/annotating-webhook
RUN chmod +x /usr/local/bin/annotating-webhook

ENTRYPOINT ["annotating-webhook"]