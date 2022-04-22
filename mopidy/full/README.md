# Mopidy

A full [mopidy](https://github.com/mopidy/mopidy) container with __my__ preferred extensions enabled.

The [base image](../base/Dockerfile) is required.

## Build

```bash
# Build base if not already done
docker build -t mopidy-base ../base

# Build image
docker build -t mopidy-full .
```

## Run

```bash
docker run --rm \
	--name mopidy-full \
	<< SEE BASE IMAGE >>
	--port 6600:6600
	mopidy-full
```

Port `6600` is used for mpd.
