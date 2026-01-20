up:
	docker compose up

build:
	docker compose --progress=plain build

build-no-cache:
	docker compose --progress=plain build --no-cache

clean:
	docker compose down -v --timeout 1

clean-with-volumes:
	docker compose down --volumes -v --timeout 1
	sudo rm -rf /local0/albertm/fractal/postgres_db /local0/albertm/fractal/app


all-from-scratch: clean-with-volumes build-no-cache
	docker compose up
