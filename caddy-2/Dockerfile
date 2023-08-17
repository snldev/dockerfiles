#syntax=docker/dockerfile:1.4
#
# A caddy 2 image supporting acme dns-01 challenges with cloudflare.
#
ARG CADDY_VERSION=2.6

FROM caddy:${CADDY_VERSION}-builder-alpine AS builder
RUN xcaddy build \
  --with github.com/caddy-dns/cloudflare@a9d3ae2690a1d232bc9f8fc8b15bd4e0a6960eec \
  ;

FROM caddy:${CADDY_VERSION}-alpine
COPY --from=builder --link /usr/bin/caddy /usr/bin/caddy
