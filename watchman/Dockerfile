FROM debian:sid
MAINTAINER Jessica Frazelle <jess@docker.com>

RUN apt-get update && apt-get install -y \
	ca-certificates \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

RUN buildDeps=' \
		autoconf \
		automake \
		clang \
		git \
		make \
	' \
	&& set -x \
	&& apt-get update && apt-get install -y $buildDeps --no-install-recommends \
	&& rm -rf /var/lib/apt/lists/* \
	&& git clone https://github.com/facebook/watchman.git /usr/src/watchman \
	&& cd /usr/src/watchman \
	&& ./autogen.sh \
	&& ./configure \
	&& make \
	&& make install \
	&& rm -rf /usr/src/watchmen \
	&& apt-get purge -y --auto-remove $buildDeps

ENTRYPOINT [ "watchman" ]
