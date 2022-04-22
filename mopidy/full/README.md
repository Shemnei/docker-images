# Mopidy

A full [mopidy](https://github.com/mopidy/mopidy) container with __my__ preferred extensions enabled.

The [base image](../base/Dockerfile) is required.

## Extensions

For a list of all installed extensions see [here](requirements.txt).

For settings of these extensions see [here](https://mopidy.com/ext/).

## Build

```bash
# Build base if not already done
docker build -t mopidy-base ../base

# Build image
docker build -t mopidy-full .
```

## Docker

__Ports:__

- `6680/tcp`: webui
- `6600/tcp`: mpd

__Volumes:__

- `/config`: Config directory (expects a `mopidy.conf` in it)
- `/var/lib/mopidy/playlists`: Playlist files in `m3u` format
- `/var/lib/mopidy/media`: Local media files

## Run

```bash
docker run --rm \
	--name mopidy-full \
	<< SEE BASE IMAGE >>
	--port 6600:6600
	mopidy-full
```

For more configurations/commands see the [Makefile](Makefile) or the [base image](../base).
