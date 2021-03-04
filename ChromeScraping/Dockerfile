from debian:buster-slim

# install chrome deps, chromedriver deps, python
RUN apt-get update
RUN apt-get install -y \
    # chrome dependencies
    apt-transport-https \
    apt-utils \
    ca-certificates \
    # needed to install chromedriver
    curl \
    wget \
    unzip \
    gnupg \
    # chromedriver dependencies
    libxcb1 \
    libnss3 \
    libglib2.0-0 \
    # python
    python3 \
    python3-pip \
    --no-install-recommends \
    # install google chrome
    && curl -sSL https://dl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && echo "deb https://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chome.list \
    && apt-get update && apt-get install -y google-chrome-stable

RUN export CHROME_VERSION=$(google-chrome --version | awk '{ print $3 }' | awk -F. 'BEGIN {OFS=".";} { print $1,$2,$3 }') \
    && export CHROME_DRIVER_VERSION=$(curl -s https://chromedriver.storage.googleapis.com/LATEST_RELEASE_${CHROME_VERSION}) \
    && wget https://chromedriver.storage.googleapis.com/${CHROME_DRIVER_VERSION}/chromedriver_linux64.zip
RUN unzip chromedriver_linux64.zip
RUN mv chromedriver /usr/local/bin

RUN rm -f chromedriver_linux64.zip

# setup python environment
RUN pip3 install selenium
RUN groupadd -r scraper && useradd -r -g scraper scraper && mkdir -p /home/scraper \
    && chown -R scraper:scraper /home/scraper
RUN chown scraper:scraper /usr/local/bin/chromedriver

RUN mkdir /home/scraper/python && chown scraper:scraper /home/scraper/python

USER scraper

ENTRYPOINT ["python3", "/home/scraper/python/scraper.py"]
