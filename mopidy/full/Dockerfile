FROM mopidy-base

# Switch to root to install
USER root

# Install extensions requirements
RUN set -eux pipefail \
  && apt-get update \
  && apt-get install -y \
    libspotify-dev \
    libspotify12 \
    python3-spotify \
  # Clean-up
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* ~/.cache

# Allow mopidy user to run system commands (restart, local scan, etc)
# REQUIRED by iris
RUN echo "mopidy ALL=NOPASSWD: /usr/local/lib/python3.7/dist-packages/mopidy_iris/system.sh" >> /etc/sudoers

COPY requirements.txt /tmp/requirements.txt
RUN set -eux pipefail \
  && chmod o+r /tmp/requirements.txt

USER mopidy

# Install extensions
RUN set -eux pipefail \
  && python3 -m pip install --no-cache-dir --upgrade pip \
  && python3 -m pip install --no-cache-dir -r /tmp/requirements.txt --upgrade

# MPD port
EXPOSE 6600
