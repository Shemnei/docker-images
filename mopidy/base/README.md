# Mopidy

A [mopidy](https://github.com/mopidy/mopidy) container as base for other containers.

__THIS IMAGE HAS NO ADDITIONAL EXTENSIONS INSTALLED BESIDES THE BUNDLED ONES.__
For an image with extensions see [here](../full).

Related/Inspirations:

- <https://github.com/nolte/docker-mopidy>
- <https://github.com/wernight/docker-mopidy>

## Build

```bash
docker build -t mopidy-base .
```

## Docker

__Ports:__

- `6680/tcp`: webui

__Volumes:__

- `/config`: Config directory (expects a `mopidy.conf` in it)
- `/var/lib/mopidy/playlists`: Playlist files in `m3u` format

## Run

Native sound:

```bash
docker run --rm \
	--name mopidy-base \
	--user root \
	--volume <CONFIG_DIR>:/config \
	--volume <PLAYLISTS_DIR>:/var/lib/mopidy/playlists \
	--publish 6680:6680 \
	--device /dev/snd \
	mopidy-base
```

Pulse native:

```bash
docker run --rm \
	--name mopidy-base \
	--user root \
	--volume <CONFIG_DIR>:/config \
	--volume <PLAYLISTS_DIR>:/var/lib/mopidy/playlists \
	--volume /run/user/$UID/pulse:/run/user/105/pulse \
	--publish 6680:6680 \
	mopidy-base
```

For more/up-to-date commands look at the [Makefile](Makefile).

## Config

This image will create a default config at `/config/mopidy.conf`.
