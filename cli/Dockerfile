# https://hub.docker.com/_/ubuntu
# 20.04 = focal
FROM ubuntu:20.04

# Update packages (bust cache)
ENV REFRESHED_AT 2020-10-08
# https://stackoverflow.com/questions/49049949/how-to-accept-license-agreement-during-docker-build
ENV DEBIAN_FRONTEND noninteractive
ENV DEBIAN_FRONTEND teletype
ENV ACCEPT_EULA Y

# Install prerequisites for fileconverter
RUN apt-get update \
    && apt-get install -y \
          php-cli php-xml php-dev php-pear php-curl php-gd php-zip php-imagick \
          libmcrypt-dev python3-pip imagemagick \
	      phantomjs xvfb jpegoptim wkhtmltopdf yui-compressor pandoc \
          npm ruby-sass optipng htmldoc pdftk zip html2text \
          git uuid-dev make msttcorefonts \
          libemail-outlook-message-perl unoconv \
    && rm -rf /var/lib/apt/lists/*

# Missing: python-reportlab python-gpgme ruby-compass php-xsl

# PHP utilities
RUN pecl channel-update pecl.php.net \
    && curl -sS https://getcomposer.org/installer -o composer-setup.php \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && pecl install mcrypt

# Other converters
RUN pip3 install xhtml2pdf

# Clone php-file-converters
ENV REFRESHED_AT 2020-10-08
RUN git clone https://github.com/brainite/php-file-converters.git /usr/share/fileconverter \
    && cd /usr/share/fileconverter && composer install \
    && ln -s /usr/share/fileconverter/bin/fileconverter /usr/local/bin/fileconverter

# Update configurations
ADD etc/ImageMagick-6/policy.xml /etc/ImageMagick-6/policy.xml
ENV MAGICK_CONFIGURE_PATH /etc/ImageMagick-6
ENV QT_QPA_PLATFORM vnc

# Allow the system to start in /work.    
RUN mkdir /work
WORKDIR /work
VOLUME ["/work"]
ENTRYPOINT ["fileconverter"]
