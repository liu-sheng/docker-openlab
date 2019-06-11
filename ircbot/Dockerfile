FROM ubuntu:latest

MAINTAINER liusheng <liusheng2048@gmail.com>

ENV SUPYBOT_HOME=/home/supybot \
    SUPYBOT_IDENT=supybot \
    SUPYBOT_NETWORK=freenode \
    SUPYBOT_NICK=supybot \
    SUPYBOT_PORT=6697 \
    SUPYBOT_PREFIXES=! \
    SUPYBOT_SERVER=irc.freenode.net \
    SUPYBOT_USER=supybot \
    SUPYBOT_USE_SSL=True \
    SUPYBOT_OWNER=owner \
    SUPYBOT_OWNER_PASS=owner \
    LANG=C

RUN useradd -u 1001 -g 0 -d ${SUPYBOT_HOME}/ -m -r -s /usr/sbin/nologin supybot
RUN mkdir -p ${SUPYBOT_HOME}/backup ${SUPYBOT_HOME}/data/tmp ${SUPYBOT_HOME}/logs/plugins ${SUPYBOT_HOME}/plugins ${SUPYBOT_HOME}/tmp
RUN apt-get git-core python-pip
RUN git clone https://github.com/ProgVal/Limnoria.git /tmp/Limnoria
RUN cd /tmp/Limnoria
RUN pip -q install -r requirements.txt
RUN python ./setup.py -q install
RUN apt-get clean
RUN cd $HOME
RUN rm -rf /tmp/Limnoria
