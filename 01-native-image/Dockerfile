FROM container-registry.oracle.com/os/oraclelinux:9-slim

ARG APP_FILE
EXPOSE 8080

COPY ${APP_FILE} app
ENTRYPOINT ["/app"]