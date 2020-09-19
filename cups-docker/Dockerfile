FROM balenalib/raspberry-pi-debian:buster

RUN [ "cross-build-start" ]

LABEL description="Raspbian (buster) with CUPS"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \
  && apt-get install -y \
    vim \
    locales \
    whois \
    cups \
    cups-client \
    cups-bsd \
    printer-driver-all \
    printer-driver-gutenprint \
    hpijs-ppds \
    hp-ppd  \
    hplip \
    printer-driver-foo2zjs \
  && useradd \
    --groups=sudo,lp,lpadmin \
    --create-home \
    --home-dir=/home/print \
    --shell=/bin/bash \
    --password=$(mkpasswd print) \
    print \
  && sed -i '/%sudo[[:space:]]/ s/ALL[[:space:]]*$/NOPASSWD:ALL/' /etc/sudoers \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && mkdir /var/lib/apt/lists/partial

COPY etc-cups/cupsd.conf /etc/cups/cupsd.conf

EXPOSE 631

ENTRYPOINT ["/usr/sbin/cupsd", "-f"]

RUN [ "cross-build-end" ]
