FROM ubuntu:latest

MAINTAINER liusheng <liusheng2048@gmail.com>

ENV SUPYBOT_HOME=/home/supybot \
    SUPYBOT_IDENT=supybot \
    SUPYBOT_NETWORK=freenode \
    SUPYBOT_PORT=6697 \
    SUPYBOT_PREFIXES="" \
    SUPYBOT_SERVER=irc.freenode.net \
    SUPYBOT_OWNER=owner \
    SUPYBOT_OWNER_PASS=owner \
    SUPYBOT_USER=openlab \
    SUPYBOT_PASSWORD="" \
    SUPYBOT_NICK=openlab \
    SUPYBOT_USE_SSL=True \
    SUPYBOT_CHANNELS=#askopenlab \
    LANG=C

RUN useradd -u 1001 -g 0 -d ${SUPYBOT_HOME}/ -m -r -s /bin/bash supybot
RUN mkdir -p ${SUPYBOT_HOME}/backup ${SUPYBOT_HOME}/data/tmp ${SUPYBOT_HOME}/logs/plugins ${SUPYBOT_HOME}/plugins ${SUPYBOT_HOME}/tmp
RUN apt-get update && apt-get install git-core python-pip gettext -y
RUN pip install git+https://github.com/ProgVal/Limnoria
RUN apt-get autoremove -y && apt-get clean -y && rm -fr /var/lib/apt/lists/*

COPY openlab-ircbot.conf.template ${SUPYBOT_HOME}/
RUN cd ${SUPYBOT_HOME} && envsubst < "openlab-ircbot.conf.template" > "openlab-ircbot.conf"
RUN git clone https://github.com/rkdarst/MeetBot /tmp/MeetBot && \
    cp -r /tmp/MeetBot/MeetBot ${SUPYBOT_HOME}/plugins/ && \
    cp -r /tmp/MeetBot/ircmeeting ${SUPYBOT_HOME}/plugins/MeetBot/ && \
    rm -fr /tmp/MeetBot

RUN git clone https://github.com/ProgVal/Supybot-plugins /tmp/Supybot-plugins && \
    cp -r /tmp/Supybot-plugins/GitHub ${SUPYBOT_HOME}/plugins/ && \
    rm -fr /tmp/Supybot-plugins

RUN chown -R 1001:0 ${SUPYBOT_HOME} && \
    chmod -R 666 ${SUPYBOT_HOME} && \
    find ${SUPYBOT_HOME} -type d -exec chmod 777 {} +

USER 1001

WORKDIR ${SUPYBOT_HOME}
CMD supybot openlab-ircbot.conf
