all: build run

login:
	docker login --username=${USER} ghcr.io --password-stdin
pull:
	docker pull ghcr.io/eth-cscs/slurm-container-20.11.9:latest

build:
	(cd .. &&\
	docker build \
		-f docker/Dockerfile \
		-t slurm-uenv-mount:latest .)

run:
	(cd .. &&\
	docker run -it --rm \
	    --name slurm-uenv-mount \
	    --privileged \
	    --volume `pwd`/:/slurm-uenv-mount:ro \
	    slurm-uenv-mount:latest /testuser-entrypoint.sh bash)

run-detach:
	docker run --detach -it --name slurm-uenv-mount --rm --privileged slurm-uenv-mount:latest /testuser-entrypoint.sh bash

run-root:
	(cd .. &&\
	docker run -it --rm \
	    --name slurm-uenv-mount \
	    --privileged \
	    --volume `pwd`/:/slurm-uenv-mount:ro \
	    slurm-uenv-mount:latest bash)

exec:
	docker exec -it -u testuser slurm-uenv-mount bash -l
