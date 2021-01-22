FROM jenkins/inbound-agent:4.6-1

USER root

ARG TIMEZONE="Asia/Shanghai"
RUN echo ${TIMEZONE} > /etc/timezone; \
    rm /etc/localtime; \
    dpkg-reconfigure -f noninteractive tzdata

ARG CHROME_VERSION="google-chrome-stable"
RUN apt-get update; \
    apt-get install -y \
    build-essential \
    curl \
    git \
    libffi-dev \
    libgdbm-dev \
    libncurses5-dev \
    libnss3-dev \
    libreadline-dev \
    libssl-dev \
    python3-pip \
    python3-dev \
    ttf-wqy-microhei \
    ttf-wqy-zenhei \
    unzip \
    xfonts-wqy \
    zip \
    zlib1g-dev; \
    wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | apt-key add -; \
    echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list; \
    apt-get update; \
    apt-get -y install --no-install-recommends ${CHROME_VERSION:-google-chrome-stable}; \
    rm /etc/apt/sources.list.d/google-chrome.list; \
    rm -rf /var/lib/apt/lists/*

COPY requirements.txt /opt
RUN pip3 install --no-cache-dir -r /opt/requirements.txt
