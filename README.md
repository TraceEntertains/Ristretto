# Ristretto

Ristretto is a plugin for Aroma that provides a foundation for smart home automation on the Wii U with a HTTP server. This will allow for other devices to communicate with the Wii U, and can then be used with something like [homebridge-wiiu](https://github.com/ItzSwirlz/homebridge-wiiu) to be added to existing home automation software.

Currently, it is still a work-in-progress. This code is currently made specifically for my setup and will eventually be generalized.

## Installation

(`[ENVIRONMENT]` is a placeholder for the actual environment name.)

1. Copy the file `ExamplePlugin.wps` into `sd:/wiiu/environments/[ENVIRONMENT]/plugins`.
2. Requires the [WiiUPluginLoaderBackend](https://github.com/wiiu-env/WiiUPluginLoaderBackend) in `sd:/wiiu/environments/[ENVIRONMENT]/modules`.

Start the environment (e.g Aroma) and the backend should load the plugin.

## Building

For building you need:

- [wups](https://github.com/Maschell/WiiUPluginSystem)
- [wut](https://github.com/devkitpro/wut)

Install them (in this order) according to their README's. Don't forget the dependencies of the libs itself.

Then you should be able to compile via `make` (with no logging) or `make DEBUG=1` (with logging).

## Buildflags

### Logging

Building via `make` only logs errors (via OSReport). To enable logging via the [LoggingModule](https://github.com/wiiu-env/LoggingModule) set `DEBUG` to `1` or `VERBOSE`.

`make` Logs errors only (via OSReport).
`make DEBUG=1` Enables information and error logging via [LoggingModule](https://github.com/wiiu-env/LoggingModule).
`make DEBUG=VERBOSE` Enables verbose information and error logging via [LoggingModule](https://github.com/wiiu-env/LoggingModule).

If the [LoggingModule](https://github.com/wiiu-env/LoggingModule) is not present, it'll fallback to UDP (Port 4405) and [CafeOS](https://github.com/wiiu-env/USBSerialLoggingModule) logging.

## Building using the Dockerfile

It's possible to use a docker image for building. This way you don't need anything installed on your host system.

```
# Build docker image (only needed once)
docker build . -t example-plugin-builder

# make
docker run -it --rm -v ${PWD}:/project example-plugin-builder make DEBUG=1

# make clean
docker run -it --rm -v ${PWD}:/project example-plugin-builder make clean
```

## Format the code via docker

`docker run --rm -v ${PWD}:/src ghcr.io/wiiu-env/clang-format:13.0.0-2 -r ./src -i`
