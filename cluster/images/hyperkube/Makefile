# build the hyperkube image.

VERSION=$(shell git rev-parse --short HEAD)
ARCH=amd64
BASEIMAGE=debian:jessie

## Comment in for arm builds, must be run on an arm machine
# ARCH=arm
# need to escape '/' for the regexp below
# BASEIMAGE=armbuild\\/debian:jessie

all: build

build:
	cp ../../saltbase/salt/helpers/safe_format_and_mount .
	cp ../../saltbase/salt/generate-cert/make-ca-cert.sh  .
	cp ../../../_output/dockerized/bin/linux/amd64/hyperkube .
	sed -i '' "s/VERSION/${VERSION}/g" master-multi.json master.json kube-proxy.json
	sed -i '' "s/ARCH/${ARCH}/g" master-multi.json master.json kube-proxy.json
	sed -i '' "s/BASEIMAGE/${BASEIMAGE}/g" Dockerfile
	docker build -t huggsboson/hyperkube:${VERSION} .

clean:
	rm -f safe_format_and_mount make-ca-cert.sh hyperkube

.PHONY: all build clean
