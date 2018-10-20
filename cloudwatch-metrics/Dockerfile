FROM alpine:3.5

RUN apk add --no-cache coreutils perl-libwww perl-datetime perl-lwp-protocol-https perl-net-ssleay && \
    wget http://aws-cloudwatch.s3.amazonaws.com/downloads/CloudWatchMonitoringScripts-1.2.2.zip && \
    unzip CloudWatchMonitoringScripts-1.2.2.zip && \
    rm CloudWatchMonitoringScripts*.zip

WORKDIR aws-scripts-mon

COPY docker-entrypoint.sh docker-entrypoint.sh
RUN chmod +x docker-entrypoint.sh

CMD ./docker-entrypoint.sh
