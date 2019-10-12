ARG ARCH_TAG

FROM seancheung/alpinewine:x11$ARCH_TAG
LABEL maintainer="Sean Cheung <theoxuanx@gmail.com>"

RUN set -ex && \
    echo "Installing dependencies..." && \
    apk add --no-cache bash && \
    export repo_mirror=$(head -1 /etc/apk/repositories | sed -n 's/\/alpine.*$//p') && \
    apk add --no-cache -X $repo_mirror/alpine/edge/testing novnc && \
    echo "Clean Up..." && \
    rm -rf /var/cache/apk/*

COPY novnc.conf /etc/supervisor/conf.d/

EXPOSE 8080