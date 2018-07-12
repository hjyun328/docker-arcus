# image
FROM arcus-ubuntu:14.04

# maintainer
MAINTAINER hjyun <hjyun328@gmail.com>

# env
ENV ARCUS_PATH        /usr/lib/arcus
ENV ARCUS_USER        arcus
ENV ZOOKEEPER_PATH    $ARCUS_PATH/zookeeper

# add arcus user
RUN useradd -d $ARCUS_PATH -c ARCUS -s /bin/bash $ARCUS_USER
RUN rm -rf $ARCUS_PATH/*
RUN echo "$ARCUS_USER:$ARCUS_USER" : chpasswd

# download arcus
WORKDIR /usr/lib
RUN git clone https://github.com/naver/arcus.git
RUN chown -R $ARCUS_USER:$ARCUS_USER $ARCUS_PATH

# build arcus
USER $ARCUS_USER
WORKDIR $ARCUS_PATH/scripts
RUN ./build.sh

# entrypoint & cmd
WORKDIR $ARCUS_PATH
COPY file/entrypoint.sh /
ENTRYPOINT ["/entrypoint.sh"]
CMD ["$ZOOKEEPER_PATH/bin/zkServer.sh", "start-foreground"]
