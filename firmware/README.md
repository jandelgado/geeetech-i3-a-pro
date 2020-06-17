# dockerized marlin firmware builder

Simple dockerized environment to build and upload a [marlin](https://marlinfw.org) 3D-Printer firmware, controlled by a makefile.

The [firmware is built using a docker container](Dockerfile) which uses [platformio](https://platformio.org).

Targets:

```sh
$ make
marlin docker builder
usage: make TARGET [TTY=tty] [CONFIG=config]
  available targets: build-docker-image, build, upload, shell, terminal
using tty=/dev/ttyUSB0 and config=Configuration-e3dv6.h
```

Example usage:

```sh
$ make build-docker-image  # run once first to build the docker image
$ make build  # build the firmware
$ make upload PORT=/dev/ttyUSB0   # build firmware and upload 
$ make terminal  # run a shell on the default 
$ make clean  # remove platformio downloaded files
$ make shell  # start a shell in the build container
```

This directory also contains my 2 Marlin configurations:
* [configuration for the original Geeetech I3A Pro printer](Configuration.h)
* [configuration for the E3Dv6/bowden modified printer](Configuration-e3dv6.h)

See [README.md](../README.md) for details regarding the 3D-Printer.

## License

MIT

## Author 

(c) 2020 by Jan Delgado

