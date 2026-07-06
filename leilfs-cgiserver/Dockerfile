ARG BASE_IMAGE=leilfs-base
FROM $BASE_IMAGE

# SAUNAFS_VERSION: pin a specific version (e.g. "3.14.0") or leave empty for latest
ARG SAUNAFS_VERSION=""

# Install the specified LeilFS package
RUN apt-get update && \
	PKG="saunafs-cgiserv${SAUNAFS_VERSION:+=$SAUNAFS_VERSION}" && \
	apt-get install -y "$PKG" && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/*

# Since 5.10, -H is the local bind address (default: any), no longer the
# master host — the master is passed as a URL query param by the browser.
CMD ["/usr/bin/python3", "/usr/sbin/saunafs-cgiserver", "-v", "-P", "9425"]
