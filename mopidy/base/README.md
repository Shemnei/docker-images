# Mopidy

A [mopidy](https://github.com/mopidy/mopidy) container as base for other containers.

__THIS IMAGE HAS NO ADDITIONAL EXTENSIONS INSTALLED BESIDES THE BUNDLED ONES.__

The `Dockerfile` is inspired by <https://github.com/nolte/docker-mopidy> and <https://github.com/wernight/docker-mopidy> but with all extensions removed.

## Build

```bash
docker build -t mopidy-base .
```

## Run

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

Both volumes are optional.
The port is used for the `http` extension (web-ui).

## Config

This image will create a default config at `/config/mopidy.conf`.
