.PHONY: build clean run run-pulse

build:
	docker stop mopidy-full || true
	docker rm mopidy-full || true

clean:
	docker build -t mopidy-base ../base
	docker build -t mopidy-full .

run:
	docker run --rm \
		--name mopidy-full \
		--user root \
		--publish 6680:6680 \
		--publish 8080:6600 \
		--volume ./.private/config/mopidy.conf:/config/mopidy.conf:ro \
		--volume ./.private/media:/var/lib/mopidy/media:ro \
		--device /dev/snd \
		mopidy-full

run-pulse:
	docker run --rm \
		--name mopidy-full \
		--user root \
		--publish 6680:6680 \
		--publish 8080:6600 \
		--volume ./.private/config/mopidy.conf:/config/mopidy.conf:ro \
		--volume ./.private/media:/var/lib/mopidy/media:ro \
		--volume /run/user/$(UID)/pulse:/run/user/105/pulse \
		--device /dev/snd \
		mopidy-full
