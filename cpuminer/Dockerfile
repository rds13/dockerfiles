FROM alpine:latest
MAINTAINER Jessie Frazelle <jess@linux.com>

RUN apk add --no-cache \
	ca-certificates \
	curl \
	openssl

ENV CPUMINER_VERSION v2.4.5
RUN set -x \
	&& apk add --no-cache --virtual .build-deps \
		autoconf \
		automake \
		build-base \
		curl-dev \
		git \
		openssl-dev \
	&& git clone --branch "${CPUMINER_VERSION}" https://github.com/pooler/cpuminer.git /usr/src/cpuminer \
	&& ( \
	cd /usr/src/cpuminer \
	&& ./autogen.sh \
	&& ./configure CFLAGS="-O3" \
	&& make \
	&& make install \
	) \
	&& rm -rf /usr/src/cpuminer \
	&& apk del .build-deps

ENTRYPOINT [ "minerd" ]
