FROM alpine:3.17

ARG PKG="git vim curl unzip zip sudo bash"

RUN apk update && \
    apk add --no-cache ${PKG}

ARG USERNAME=vscode
ARG USER_GROUP_NAME=workspace
ARG USER_UID=1000
ARG USER_GID=1000

SHELL ["/bin/bash", "-c"]

RUN addgroup --system --gid ${USER_GID} ${USER_GROUP_NAME} \
    && adduser --system --disabled-password --home /home/${USERNAME} \
    --uid ${USER_UID} --shell /bin/bash --ingroup ${USER_GROUP_NAME} ${USERNAME} \
    && echo "${USER_GROUP_NAME}	ALL=(ALL:ALL) NOPASSWD: ALL" >> /etc/sudoers.d/${USER_GROUP_NAME} \
    && chmod 0440 /etc/sudoers.d/${USER_GROUP_NAME}

ARG JAVA_VERSION=17.0.9-amzn
ARG GRADLE_VERSION=8.5

ARG SDKMAN_DIR=/home/vscode/.sdkman

USER vscode
RUN curl -s "https://get.sdkman.io" | bash \
    && source ${SDKMAN_DIR}/bin/sdkman-init.sh \
    && sdk install java ${JAVA_VERSION} \
    && sdk install gradle ${GRADLE_VERSION}
