SRC_NAME := v2ray-5.16.1
SRC_URL := https://github.com/v2fly/v2ray-core/archive/refs/tags/v5.16.1.tar.gz

THISDIR = $(shell pwd)

all: download_test extract_test build

download_test:
	( if [ ! -f $(SRC_NAME).tar.gz ]; then \
		wget -t5 --timeout=20 --no-check-certificate -O $(SRC_NAME).tar.gz $(SRC_URL); \
	fi )

extract_test:
	( if [ ! -d $(SRC_NAME) ]; then \
		mkdir -p $(SRC_NAME); \
		tar xf $(SRC_NAME).tar.gz -C $(SRC_NAME) --strip-components=1; \
	fi )

build:
	( cd $(SRC_NAME)/main; \
	GOOS=linux GOARCH=mipsle go build -gcflags=all="-l" -ldflags "-w -s -buildid=" -trimpath -o $(THISDIR)/v2ray; \
	)

clean:
	rm -rf $(SRC_NAME)
	rm -f v2ray

romfs:
	$(ROMFSINST) -p +x $(THISDIR)/v2ray /usr/bin/v2ray