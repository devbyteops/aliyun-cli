FROM alpine:3.20.2
ARG ALIYUN_VERSION=3.0.216
RUN apk update && apk add --no-cache bash
RUN wget https://aliyuncli.alicdn.com/aliyun-cli-linux-${ALIYUN_VERSION}-amd64.tgz && \
    tar -xvzf aliyun-cli-linux-${ALIYUN_VERSION}-amd64.tgz && \
    rm aliyun-cli-linux-${ALIYUN_VERSION}-amd64.tgz && \
    mv aliyun /usr/local/bin/
# As we are using Alpine Linux, following command will create a separate symbolic link to lib64 dynamic libraries.
RUN mkdir /lib64 && ln -s /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2

# Create the app user & Configure working directory
ARG USER_NAME=appuser
ARG USER_UID=1000
ARG USER_GID=$USER_UID
RUN addgroup --gid $USER_GID $USER_NAME \
    && adduser -D -S -G $USER_NAME -u $USER_UID $USER_NAME \
    && mkdir /home/$USER_NAME/app && chown -R $USER_UID:$USER_GID /home/$USER_NAME/app && chmod -R 755 /home/$USER_NAME/app
WORKDIR /home/$USER_NAME/app
USER $USER_NAME