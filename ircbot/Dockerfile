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

RUN useradd -u 1001 -g 0 -d ${SUPYBOT_HOME}/ -m -r -s /usr/sbin/nologin supybot
RUN mkdir -p ${SUPYBOT_HOME}/backup ${SUPYBOT_HOME}/data/tmp ${SUPYBOT_HOME}/logs/plugins ${SUPYBOT_HOME}/plugins ${SUPYBOT_HOME}/tmp
RUN apt-get update && apt-get install git-core python-pip -y
RUN pip install git+https://github.com/ProgVal/Limnoria
RUN apt-get autoremove -y && apt-get clean -y
RUN cd $HOME

COPY openlab-ircbot.conf.template ${SUPYBOT_HOME}/
RUN cd ${SUPYBOT_HOME}
RUN eval "cat <<EOF \
    $(< openlab-ircbot.conf.template) \
    EOF" > openlab-ircbot.conf