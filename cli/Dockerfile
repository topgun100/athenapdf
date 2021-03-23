FROM debian:10
MAINTAINER Arachnys <techteam@arachnys.com>

RUN echo 'deb http://httpredir.debian.org/debian/ stable main contrib non-free' >> /etc/apt/sources.list

RUN apt-get -yq update && \
    apt-get -yq install \
        wget \
        xvfb \
        libgconf-2-4 \
        libgtk2.0-0 \
        libnotify4 \
        libnss3 \
        libxss1 \
        libxtst6 \
        libasound2 \
        culmus \
        fonts-beng \
        fonts-dejavu \
        fonts-hosny-amiri \
        fonts-lklug-sinhala \
        fonts-lohit-guru \
        fonts-lohit-knda \
        fonts-samyak-gujr \
        fonts-samyak-mlym \
        fonts-samyak-taml \
        fonts-sarai \
        fonts-sil-abyssinica \
        fonts-sil-padauk \
        fonts-telu \
        fonts-thai-tlwg \
        fonts-unfonts-core \
        ttf-wqy-zenhei \
        multiarch-support \
    && apt-get -yq autoremove \
    && apt-get -yq clean \
    && rm -rf /var/lib/apt/lists/* \
    && truncate -s 0 /var/log/*log

COPY fonts.conf /etc/fonts/conf.d/100-athena.conf

COPY build/athenapdf-linux-x64/ /athenapdf/
RUN wget http://ftp.de.debian.org/debian/pool/main/libp/libpng/libpng12-0_1.2.50-2+deb8u3_amd64.deb && \
    wget http://ftp.de.debian.org/debian/pool/main/f/fonts-liberation/fonts-liberation_1.07.4-1_all.deb && \
    wget http://ftp.de.debian.org/debian/pool/main/f/freetype/libfreetype6_2.5.2-3+deb8u2_amd64.deb && \
    wget http://ftp.de.debian.org/debian/pool/main/c/cairo/libcairo2_1.14.0-2.1+deb8u2_amd64.deb && \
    wget http://ftp.de.debian.org/debian/pool/main/p/pango1.0/libpangocairo-1.0-0_1.36.8-3_amd64.deb && \
    dpkg -i *.deb
WORKDIR /athenapdf/

ENV PATH /athenapdf/:$PATH

COPY entrypoint.sh /athenapdf/entrypoint.sh

RUN mkdir -p /converted/
WORKDIR /converted/

CMD ["athenapdf"]

ENTRYPOINT ["/athenapdf/entrypoint.sh"]
