# run with
# docker run --rm -it -v $PWD:/root gaborsomogyi/ffmpeg

FROM ubuntu:bionic

LABEL maintainer='Gábor Somogyi'

# install curl and gpg2 to be able to verify the signing key
RUN apt-get update && \
    apt-get install -y gnupg2

# get the signing key and add the ppa
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 4AB0F789CBA31744CC7DA76A8CF63AD3F06FC659 && \
    echo 'deb http://ppa.launchpad.net/jonathonf/ffmpeg-4/ubuntu bionic main' >> /etc/apt/sources.list

# install the latest ffmpeg
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y ffmpeg

WORKDIR /root
