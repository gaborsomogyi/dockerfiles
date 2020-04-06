# run with
# docker run --rm -it -v $PWD:/root gaborsomogyi/mpv

FROM ubuntu:bionic

LABEL maintainer='Gábor Somogyi'

# install curl and gpg2 to be able to verify the key
RUN apt-get update && \
    apt-get install -y gnupg2 curl

# get the key and add the uvt repo
RUN curl -L https://non-gnu.uvt.nl/debian/uvt_key.asc | apt-key add - && \
    echo 'deb http://non-gnu.uvt.nl/debian bionic uvt' >> /etc/apt/sources.list

# install the latest mpv
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -t bionic -y mpv

WORKDIR /root
