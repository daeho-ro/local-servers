FROM alpine:latest

ENV SLEEP 60
RUN apk update && apk add terraform bash

VOLUME [ "/data" ]
WORKDIR /data

CMD bash -c "terraform init; terraform plan -out=main.plan; while !(terraform apply -auto-approve main.plan); do sleep ${SLEEP}; done"
