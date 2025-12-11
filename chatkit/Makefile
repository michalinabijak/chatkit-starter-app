.PHONY: build run

build:
	docker build -t chatkit-dev -f Dockerfile ../..

run:
	docker run --rm --env-file .env.local -p 3000:3000 chatkit-dev
