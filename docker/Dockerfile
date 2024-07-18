FROM python:3.12-slim-bookworm

WORKDIR /install

RUN apt update && apt install -y \
    python3-distutils \
    python3-pip \
    sudo

RUN apt update && apt install -y \ 
    ffmpeg \
    libosmesa6-dev

COPY docker/requirements.txt requirements.txt
RUN pip3 install -r requirements.txt


ENV MYUSER=ubuntu
ENV MYGID=1000
ENV MYUID=1000

RUN groupadd -g ${MYGID} ${MYUSER}
RUN useradd -u ${MYUID} -g ${MYGID} -p $(perl -e 'print crypt($ARGV[0], "password")' 'password') -G adm,sudo ${MYUSER} && mkdir /home/${MYUSER} && chown ${MYUSER}:${MYUSER} /home/${MYUSER}

USER ${MYUSER}

EXPOSE 8888

WORKDIR /python


