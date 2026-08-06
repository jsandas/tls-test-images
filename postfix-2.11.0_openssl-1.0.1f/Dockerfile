FROM ubuntu:trusty

# Set noninteractive mode for apt-get
ENV DEBIAN_FRONTEND=noninteractive

# Update
RUN apt-get update && apt-get -y upgrade \
    && apt-get -y install postfix supervisor \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /etc/postfix/certs \
    && openssl req -x509 -newkey rsa:2048 \
    -days 365 -nodes \
    -subj "/C=US/ST=Denial/L=Springfield/O=Dis/CN=www.example.com" \
    -keyout /etc/postfix/certs/cert-rsa.key \
    -out /etc/postfix/certs/cert-rsa.crt

# Add files
COPY --chmod=+x install.sh /opt/install.sh

RUN /opt/install.sh

# Run
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]
