FROM nginx:1.22.0-alpine

# Install system dependencies
RUN apk update \
    && apk upgrade \
    && apk --update add logrotate \
    openssl \
    curl \
    bash
    
# Create system user
RUN set -x ; \
    addgroup -g 1000 -S www-data ; \
    adduser -u 1000 -D -S -G www-data www-data && exit 0 ; exit 1

ENTRYPOINT ["nginx", "-g", "daemon off;"]
