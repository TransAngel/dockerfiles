ARG DOCKER_VER=19.03
ARG COMPOSE_VER=1.24.1
ARG ALPINE_VER=3.10

################################################################################
# Source - Docker
################################################################################
FROM docker:${DOCKER_VER} AS source-docker


################################################################################
# Source
################################################################################
FROM docker/compose:${COMPOSE_VER} AS source
# Docker
COPY --from=source-docker /usr/local/bin/docker /usr/local/bin/
COPY --from=source-docker /usr/local/bin/docker-entrypoint.sh /usr/local/bin/


################################################################################
# Runtime
################################################################################
FROM frolvlad/alpine-glibc:alpine-${ALPINE_VER}
COPY --from=source /usr/local/bin/* /usr/local/bin/

RUN DEPS="bash make curl" \
    apk add $DEPS

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["sh"]
