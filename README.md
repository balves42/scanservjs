# scanservjs

## About this fork

Since i got a raspberry pi 4 laying around and an old printer, i decided to made this and share it with the world.

* Base image changed to compile for arm64
* Installed libsane-hpaio drivers (for my old HP deskjet F4180)
* run.sh script restarts dbus service (it's needed in my case)

Credit for the original project should go to [Sam Strachan](https://github.com/sbs20). 

## What i recommend

Check the [original instructions](https://github.com/sbs20/scanservjs/blob/master/docs/docker.md) for returning the 00X and 00Y and run something like this:

```sh
docker run -d \
  -p 8080:8080 \
  -v /var/run/dbus:/var/run/dbus \
  -v /docker/scanservjs/scans:/app/data/output \
  --restart always \
  --name scanservjs-rpi \
  --device /dev/bus/usb/00X/00Y:/dev/bus/usb/00X/00Y \
  brunoalves/scanservjs-rpi:arm64
```

or with "privileged" which is unsafer:

```sh
docker run -d \
  -p 8080:8080 \
  -v /var/run/dbus:/var/run/dbus \
  -v /docker/scanservjs/scans:/app/data/output \
  --restart always \
  --name scanservjs-rpi \
  --privileged brunoalves/scanservjs-rpi:arm64
```

If your device is not found, you may need to run this on your host:
```sh
sudo chmod a+rw dev/bus/usb/00X/00Y
```

[![Build Status](https://img.shields.io/github/workflow/status/sbs20/scanservjs/NodeCI?style=for-the-badge)](https://github.com/sbs20/scanservjs/actions)
[![Code QL Status](https://img.shields.io/github/workflow/status/sbs20/scanservjs/CodeQL?label=CodeQL&style=for-the-badge)](https://github.com/sbs20/scanservjs/actions)
[![Docker Image Size (latest by date)](https://img.shields.io/docker/image-size/sbs20/scanservjs?style=for-the-badge)](https://hub.docker.com/r/sbs20/scanservjs)
[![Docker Pulls](https://img.shields.io/docker/pulls/sbs20/scanservjs?style=for-the-badge)](https://hub.docker.com/r/sbs20/scanservjs)
[![GitHub stars](https://img.shields.io/github/stars/sbs20/scanservjs?label=Github%20stars&style=for-the-badge)](https://github.com/sbs20/scanservjs)
[![GitHub](https://img.shields.io/github/license/sbs20/scanservjs?style=for-the-badge)](https://github.com/sbs20/scanservjs/blob/master/LICENSE.md)

![screenshot](https://github.com/sbs20/scanservjs/raw/master/docs/screen0.jpg)

Copyright 2016-2021 [Sam Strachan](https://github.com/sbs20)

## What people are saying

> I've decided to switch to using only this, I find using this in a browser is
> just perfect and way better than bloated software from printer manufacturers


> It enabled me to still use my old hp3900 scanner without worrying about
> drivers and vendor specific UIs. Furthermore, scans just being accessible via
> an awesome web interface makes it even more brilliant!


> This is a great project! The touchscreen and buttons on my Brother scanner are
> broken, meaning the device is useless by itself because one cannot trigger
> scans, but with this project I can trigger it remotely just fine.


> Absolutely love untethering my scanner from my laptop. Also means that I know
> it will work "forever", regardless of OS updates, since its all just a docker
> container.

## About

scanservjs is a web UI frontend for your scanner. It allows you to share one or
more scanners (using SANE) on a network without the need for drivers or
complicated installation.

## Features

* Cropping
* Source selection (Flatbed / ADF)
* Resolution
* Output formats (TIF, JPG, PNG, PDF and TXT with Tesseract OCR) with varying
  compression settings
* Filters: Autolevels, Threshold, Blur
* Configurable overrides for all defaults as well as filters and formats
* Multipage scanning (with collation for double sided scans)
* International translations: Czech, Dutch, French, German, Italian, Mandarin,
  Polish, Portuguese (PT & BR), Russian, Spanish, Turkish;
  [Help requested](https://github.com/sbs20/scanservjs/issues/154)
* Light and dark mode
* Responsive design

It supports any
[SANE compatible devices](http://www.sane-project.org/sane-supported-devices.html).

## Requirements

* SANE Scanner
* Linux host (or VM with necessary pass-through e.g. USB)
* Software sane-utils, ImageMagick, Tesseract (optional) and nodejs

## Documentation

* [Manual installation](docs/install.md)
* [Docker installation](docs/docker.md)
* [Scanner and SANE setup](docs/sane.md)
* [Proxy setup](docs/proxy.md)
* [Troubleshooting](docs/troubleshooting.md)
* [Development notes](docs/development.md)
* [Configuration and device override](docs/config.md)
* [Integration](docs/integration.md)

## Why?

This is yet another scanimage-web-front-end. Why? It originally started as an
adaptation of phpsane - just to make everything a bit newer, give it a refresh
and make it work on minimal installations without imagemagick - that version is
[still available](https://github.com/sbs20/scanserv) but is no longer
maintained. Since then, I just wanted to write it in node and enhance it a bit,
and it's been a labour of love ever since.

## Acknowledgements

 * This project owes its genesis to
   [phpsane](http://sourceforge.net/projects/phpsane/)
 * [Everyone](https://github.com/sbs20/scanservjs/graphs/contributors) who has
   filed issues, tested, fixed issues, added translations and helped over the
   years. Thank you!

## More about SANE

 * http://www.sane-project.org/
