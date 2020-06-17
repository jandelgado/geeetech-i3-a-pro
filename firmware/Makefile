# build marlin images using a docker container
# Jan Delgado 06-2020
# 
.PHONY: usage build-docker-image build upload shell run terminal

TTY=/dev/ttyUSB0
CONFIG=Configuration-e3dv6.h

usage:
	@echo "marlin docker builder"
	@echo "usage: make TARGET [TTY=tty] [CONFIG=config]"
	@echo "  available targets: build-docker-image, build, upload, shell, terminal"
	@echo "using tty=${TTY} and config=${CONFIG}"

build-docker-image:
	docker build -t marlin-builder .

build: CMD:=sh -c "pio run"
build: run

upload: CMD:=sh -c "pio run --target upload --upload-port ${TTY}"
upload: run

shell: CMD:=bash
shell: run

terminal:
	picocom --imap lfcrlf -c -b 250000 ${TTY}

run:
	@test -c "${TTY}" || { echo "${TTY} not found - is printer connected?" && exit 1; }
	docker run -ti --rm \
		       -e "GOSU_UID=$(shell id -ur)" -e "GOSU_GID=$(shell id -g)"\
			   --device=${TTY} \
		       --mount type=bind,source="$(shell pwd)/Marlin",target="/marlin" \
		       --mount type=bind,source="$(shell pwd)/${CONFIG}",target="/marlin/Marlin/Configuration.h" \
			   marlin-builder \
			   ${CMD}
clean:
	rm -rf Marlin/{.pioenvs,.piolib,.piolibdeps,.platformio}
