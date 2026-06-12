REGISTRY=slavasly
VERSION=$(shell git describe --tags --abbrev=0)-$(shell git rev-parse --short HEAD)
TARGETOS=linux
TARGETARCH=amd64

format:
	gofmt -s -w ./

linux: format
	docker build -t ${TARGETOS}-${TARGETARCH} .

arm: format get
	go build .
	
macOS: format get
	go build .

Windows: format get
	go build .

image:
	docker build . -t ${REGISTRY}/${APP}:${VERSION}-${TARGETARCH}

push:
	docker push ${REGISTRY}/${APP}:${VERSION}-${TARGETARCH}

clean:
	docker rmi ${TARGETOS}-${TARGETARCH}