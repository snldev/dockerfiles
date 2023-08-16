#syntax=docker/dockerfile:1.4
#
# A caddy 2 image supporting acme dns-01 challenges with cloudflare.
#
ARG VERSION=2.6

FROM caddy:${VERSION}-builder-alpine AS builder
RUN xcaddy build \
  --with github.com/caddy-dns/cloudflare \
  ;

FROM caddy:${VERSION}-alpine
COPY --from=builder --link /usr/bin/caddy /usr/bin/caddy
