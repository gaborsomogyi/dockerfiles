# Run abevjava - the official software to file tax reports with the Hungarian authorities
#
# docker run \
# -d \
# -v ~/containers/abevjava/nyomtatvanyok:/usr/share/abevjava/nyomtatvanyok \
# -v ~/containers/abevjava/home:/root/abevjava \
# -p 5900:5900 \
# --name abevjava-vnc \
# gaborsomogyi/abevjava-vnc

FROM ubuntu:18.04

LABEL version "abevjava-vnc:2.88"
LABEL maintainer "Gábor Somogyi"

ARG DEBIAN_FRONTEND=noninteractive
ARG VNC_PASSWORD=1234

# install essentials
RUN apt-get update && \
	apt-get install -y \
	software-properties-common

# install oracle java 8 - newer versions might run into errors when authenticating
RUN add-apt-repository -y ppa:webupd8team/java && apt-get update \
	&& echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections \
	&& echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections \
	&& apt-get install -y oracle-java8-installer

RUN apt-get install -y \
	x11vnc xvfb \
	alien dpkg-dev debhelper build-essential \
	wget

# clean up
RUN rm -rf /var/lib/apt/lists/*

# setup abevjava
RUN wget https://www.nav.gov.hu/data/cms504163/abevjava_install-2.93.0-0.1.noarch.rpm \
	&& alien --scripts abevjava_install-2.93.0-0.1.noarch.rpm \
	&& dpkg -i abevjava-install_2.93.0-1.1_all.deb

# setup vnc
RUN mkdir ~/.vnc
RUN x11vnc -storepasswd $VNC_PASSWORD ~/.vnc/passwd


# autostart abevjava (might not be the best way, but it does the trick)
RUN bash -c 'echo "cd /usr/share/abevjava && ./abevjava_start" >> ~/.bashrc'

EXPOSE 5900
CMD ["x11vnc", "-forever", "-usepw", "-noxrecord", "-create"]

