build:
	docker stop mopidy-base || true
	docker rm mopidy-base || true
	docker build -t mopidy-base .

run:
	docker run --rm \
		--name mopidy-base \
		--user root \
		--publish 6680:6680 \
		--device /dev/snd \
		mopidy-base
