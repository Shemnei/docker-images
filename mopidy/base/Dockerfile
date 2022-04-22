# Adapted from <https://github.com/nolte/docker-mopidy>

FROM debian:buster-slim

RUN set -eux pipefail \
  && apt-get update \
  && apt-get install -y \
    wget \
    curl \
    #alsa-utils \
    #libasound2 \
    dumb-init \
    gnupg2 \
    libffi-dev \
    python3-distutils \
    python3-pip \
    gstreamer1.0-alsa \
    gstreamer1.0-plugins-bad \
    # Clean-up
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* ~/.cache

ARG MOPDIY_VERSION=3.2.0-1

# Dependencyies for mopidy base
RUN set -eux pipefail \
  && mkdir -p /usr/local/share/keyrings \
  && wget -q -O /usr/local/share/keyrings/mopidy-archive-keyring.gpg \
      https://apt.mopidy.com/mopidy.gpg

RUN set -eux pipefail \
  && wget -q -O /etc/apt/sources.list.d/mopidy.list https://apt.mopidy.com/buster.list

RUN set -eux pipefail \
  && apt-get update \
  && apt-get install -y \
    mopidy=${MOPDIY_VERSION} \
  # Clean-up
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* ~/.cache

# Copy the pulse-client configuratrion.
COPY pulse-client.conf /etc/pulse/client.conf

# Allows any user to run mopidy, but runs by default as a randomly generated UID/GID.
ENV HOME=/var/lib/mopidy

RUN set -eux pipefail \
  && mkdir -p /var/lib/mopidy/.config \
  && ln -s /config /var/lib/mopidy/.config/mopidy

# Default configuration
ADD mopidy.conf /var/lib/mopidy/.config/mopidy/mopidy.conf

RUN set -eux pipefail \
  && usermod -G audio,sudo mopidy

# Run as mopidy user
USER mopidy

# Basic check,
RUN /usr/bin/dumb-init /usr/bin/mopidy --version
RUN /usr/bin/dumb-init /usr/bin/mopidy config

# Playlists
VOLUME /var/lib/mopidy/playlists
# User config
VOLUME /config

EXPOSE 6680

CMD ["/usr/bin/dumb-init", "/usr/bin/mopidy"]

HEALTHCHECK --interval=5s --timeout=2s --retries=20 \
  CMD curl --connect-timeout 5 --silent --show-error --fail http://localhost:6680/ || exit 1
