.PHONY: build clean run run-pulse

build:
	docker build -t mopidy-base .

clean:
	docker stop mopidy-base || true
	docker rm mopidy-base || true

run:
	docker run --rm \
		--name mopidy-base \
		--user root \
		--publish 6680:6680 \
		--device /dev/snd \
		mopidy-base

run-pulse:
	docker run --rm \
		--name mopidy-base \
		--user root \
		--publish 6680:6680 \
		--volume /run/user/$(UID)/pulse:/run/user/105/pulse \
		mopidy-base
