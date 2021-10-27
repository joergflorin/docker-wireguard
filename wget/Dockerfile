FROM alpine:3.12.0
RUN apk add --no-cache wget=1.20.3-r1
VOLUME [ "/logs" ]
CMD wget ${url} -O /logs/${contentOut} -o /logs/${requestLog}
