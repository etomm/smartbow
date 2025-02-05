# syntax=docker/dockerfile:1

FROM ghcr.io/linuxserver/baseimage-kasmvnc:ubuntunoble

# set version label
# ARG BUILD_DATE
# ARG VERSION
# ARG CALIBRE_RELEASE
# LABEL build_version="Linuxserver.io version:- ${VERSION} Build-date:- ${BUILD_DATE}"
# LABEL maintainer="aptalca"

ENV \
  CUSTOM_PORT="8080" \
  CUSTOM_HTTPS_PORT="8443" \
  HOME="/config" \
  TITLE="Smartbow" \
  QTWEBENGINE_DISABLE_SANDBOX="1"

RUN \
  dbus-uuidgen > /etc/machine-id && \
  echo "**** install runtime packages ****" && \
  apt-get update && \
  apt-get install -y --no-install-recommends \
    dbus \
    fcitx-rime \
    fonts-wqy-microhei \
    libnss3 \
    libopengl0 \
    libqpdf29t64 \
    libxkbcommon-x11-0 \
    libxcb-cursor0 \
    libxcb-icccm4 \
    libxcb-image0 \
    libxcb-keysyms1 \
    libxcb-randr0 \
    libxcb-render-util0 \
    libxcb-xinerama0 \
    poppler-utils \
    python3 \
    python3-xdg \
    ttf-wqy-zenhei \
    wget \
    xz-utils && \
  apt-get install -y \
    speech-dispatcher  
  
RUN \
  echo "**** add icon ****" && \
  mkdir -p /opt/startapp && \
  curl -o \
    /opt/startapp/icon.ico \
    -L http://10.0.10.1:8080/favicon.ico \
	-H 'Connection: keep-alive' && \
  echo "**** install Smartbow ****" && \
  mkdir -p /tmp/smartbow && \
#  if [ -z ${CALIBRE_RELEASE+x} ]; then \
#    CALIBRE_RELEASE=$(curl -sX GET "https://api.github.com/repos/kovidgoyal/calibre/releases/latest" \
#    | jq -r .tag_name); \
#  fi && \
#  CALIBRE_VERSION="$(echo ${CALIBRE_RELEASE} | cut -c2-)" && \
#  CALIBRE_URL="https://download.calibre-ebook.com/${CALIBRE_VERSION}/calibre-${CALIBRE_VERSION}-x86_64.txz" && \
  curl -o /tmp/smartbow/linux_client \
       -L http://10.0.10.1:8080/linux_client \
	   -H 'Connection: keep-alive' && \
  chmod +x /tmp/smartbow/linux_client && \
  /tmp/smartbow/linux_client --accept && \
#  tar xvf /tmp/calibre-tarball.txz -C \
#    /opt/calibre && \
#  /opt/calibre/calibre_postinstall && \
#  printf "Linuxserver.io version: ${VERSION}\nBuild-date: ${BUILD_DATE}" > /build_version && \
  echo "**** cleanup ****" && \
  apt-get clean && \
  rm -rf \
    /tmp/* \
    /var/lib/apt/lists/* \
    /var/tmp/*
	
# add local files
COPY root/ /