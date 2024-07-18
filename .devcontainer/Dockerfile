# Note: You can use any Debian/Ubuntu based image you want. 
FROM python:3.12-slim-bookworm

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

WORKDIR /work
COPY requirements.txt requirements.txt

RUN apt update && apt install -y python3-distutils python3-pip sudo
RUN pip3 install -r requirements.txt

ENV MYUSER=danaukes
ENV MYGID=1000
ENV MYUID=1000

RUN groupadd -g ${MYGID} ${MYUSER}
RUN useradd -u ${MYUID} -g ${MYGID} -p $(perl -e 'print crypt($ARGV[0], "password")' 'test') -G adm,sudo ${MYUSER} && mkdir /home/${MYUSER} && chown ${MYUSER}:${MYUSER} /home/${MYUSER}

USER ${MYUSER}

EXPOSE 8888