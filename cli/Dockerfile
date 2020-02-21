# https://hub.docker.com/_/ubuntu
# 20.04 = focal
FROM ubuntu:20.04

# Update packages
ENV REFRESHED_AT 2020
RUN apt-get update

# Install prerequisites for fileconverter
ENV DEBIAN_FRONTEND noninteractive
ENV DEBIAN_FRONTEND teletype
RUN apt-get install -y \
    php-cli php-xsl php-dev php-pear php-curl php-gd \
    libmcrypt-dev python-pip imagemagick \
	phantomjs jpegoptim wkhtmltopdf xvfb yui-compressor pandoc \
    npm ruby-sass optipng htmldoc pdftk zip html2text \
    git uuid-dev make

# https://stackoverflow.com/questions/49049949/how-to-accept-license-agreement-during-docker-build
ENV ACCEPT_EULA Y
RUN apt-get install -y msttcorefonts

# Missing: python-reportlab python-gpgme ruby-compass

# PHP utilities
RUN pecl channel-update pecl.php.net \
    && curl -sS https://getcomposer.org/installer -o composer-setup.php \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && pecl install mcrypt

# Other converters
RUN pip install xhtml2pdf

# Clone php-file-converters
RUN git clone https://github.com/brainite/php-file-converters.git /usr/share/fileconverter \
    && cd /usr/share/fileconverter && composer install \
    && ln -s /usr/share/fileconverter/bin/fileconverter /usr/local/bin/fileconverter

# Allow the system to start in /work.    
RUN mkdir /work
WORKDIR /work
VOLUME ["/work"]
CMD ["fileconverter"]
