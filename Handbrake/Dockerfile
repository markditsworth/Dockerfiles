from ubuntu:xenial

# install add-apt-repository
RUN apt-get update && apt-get install -y software-properties-common
RUN add-apt-repository ppa:stebbins/handbrake-releases \
    && apt-get update \
    && apt-get install -y handbrake-cli

ENTRYPOINT ["HandBrakeCLI"]
