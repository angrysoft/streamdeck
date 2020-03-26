# streamdeck

A CLI application and Go library to control your Elgato Stream Deck on Linux.

If you're looking for a complete Linux service to control your StreamDeck, check
out [Deckmaster](https://github.com/muesli/deckmaster), which is based on this
library.

## Installation

Make sure you have a working Go environment (Go 1.9 or higher is required).
See the [install instructions](http://golang.org/doc/install.html).

To install streamdeck, simply run:

    go get github.com/muesli/streamdeck/cmd/...

## Configuration

On Linux you need to set up some udev rules to be able to access the device as a
regular user. Edit `/etc/udev/rules.d/99-streamdeck.rules` and add these lines:

```
SUBSYSTEM=="usb", ATTRS{idVendor}=="0fd9", ATTRS{idProduct}=="0060", MODE:="666", GROUP="plugdev"
SUBSYSTEM=="usb", ATTRS{idVendor}=="0fd9", ATTRS{idProduct}=="0063", MODE:="666", GROUP="plugdev"
SUBSYSTEM=="usb", ATTRS{idVendor}=="0fd9", ATTRS{idProduct}=="006c", MODE:="666", GROUP="plugdev"
```

Make sure your user is part of the `plugdev` group and reload the rules with
`sudo udevadm control --reload-rules`. Unplug and replug the device and you
should be good to go.

## Usage

Control the brightness, in percent between 0 and 100:

```
streamdeck-cli brightness 50
```

Set an image on the first key (from the top-left):

```
streamdeck-cli image 0 image.png
```

Clear all images:

```
streamdeck-cli clear
```

Reset the device:

```
streamdeck-cli reset
```

## Development

[![GoDoc](https://godoc.org/github.com/golang/gddo?status.svg)](https://godoc.org/github.com/muesli/streamdeck)
[![Build Status](https://travis-ci.org/muesli/streamdeck.svg?branch=master)](https://travis-ci.org/muesli/streamdeck)
[![Go ReportCard](http://goreportcard.com/badge/muesli/streamdeck)](http://goreportcard.com/report/muesli/streamdeck)
