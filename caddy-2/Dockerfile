#syntax=docker/dockerfile:1.4
#
# A caddy 2 image supporting acme dns-01 challenges with cloudflare.
#
ARG CADDY_VERSION=2.7.4

FROM caddy:${CADDY_VERSION}-builder-alpine AS builder
RUN xcaddy build \
  --with github.com/caddy-dns/cloudflare@74f004e1c1ab9056288f0baf3cd4b0039d6c77f3 \
  ;

FROM caddy:${CADDY_VERSION}-alpine
COPY --from=builder --link /usr/bin/caddy /usr/bin/caddy
