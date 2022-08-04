FROM alpine:latest

ENV PYTHONFAULTHANDLER=1 \
    PYTHONUNBUFFERED=1 \
    PYTHONHASHSEED=random \
    PIP_NO_CACHE_DIR=on \
    PIP_DISABLE_PIP_VERSION_CHECK=on

RUN apk add -v --update --no-cache \
        python3 \
        git gcc cmake libc-dev musl-dev build-base python3-dev libffi-dev \
        groff less mailcap postgresql-client && \
    python3 -m ensurepip && \
    pip3 install --upgrade pip setuptools python-magic && \
    pip3 install git+https://github.com/aws/aws-cli.git@v2 && \
    apk -v --purge del git python3-dev gcc libc-dev musl-dev build-base libffi-dev && \
    rm -rf /var/cache/apk/* && \
    adduser -D aws

USER aws
WORKDIR /home/aws
VOLUME /home/aws/.aws

ENTRYPOINT ["aws"]
