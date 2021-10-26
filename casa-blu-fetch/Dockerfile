FROM alpine:3.12.0
RUN apk add --no-cache wget=1.20.3-r1
ENTRYPOINT wget http://casa-blu.de/cgi-bin/fetch.py -O /opt/logs/fetch.out -o /opt/logs/fetch.log