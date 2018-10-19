FROM alpine:latest

RUN apk -v --update add \
        python \
        py-pip \
        groff \
        less \
        mailcap \
        postgresql-client \
        && \
    pip install --upgrade awscli==1.16.20 python-magic && \
    apk -v --purge del py-pip && \
    rm /var/cache/apk/* && \
    adduser -D aws

USER aws
WORKDIR /home/aws
VOLUME /home/aws/.aws
