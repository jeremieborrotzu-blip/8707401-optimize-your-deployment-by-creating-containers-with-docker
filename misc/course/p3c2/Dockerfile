FROM alpine:3.20

# Make the Libra application version to download configurable,
# along with the integrity checksum of the desired archive
ARG LIBRA_VERSION=0.0.3
ARG LIBRA_CHECKSUM=0d5a496622a3e6167c43d5a8edfc6d679d5e1603ce78ae48a67daaa0f5aaab5b
ARG LIBRA_REPOSITORY=https://github.com/Bornholm/libra

# Update system dependencies to reduce the risk of security vulnerabilities
# in the final image, and install the dependencies required to download
# the Libra application, pinning the desired versions
RUN apk upgrade \
    && apk add \
        wget=1.24.5-r0 \
        tar=1.35-r2

# Download the archive containing the Libra executable,
# verify the archive checksum,
# create the binary destination directory,
# extract the binary,
# then ensure it has the correct execution permissions.
RUN wget -O libra.tar.gz \
        ${LIBRA_REPOSITORY}/releases/download/v${LIBRA_VERSION}/libra_${LIBRA_VERSION}_linux_amd64.tar.gz \
    && echo "${LIBRA_CHECKSUM} libra.tar.gz" | sha256sum -c \
    && mkdir -p /usr/local/bin \
    && tar -xzf libra.tar.gz -C /usr/local/bin libra \
    && chmod +x /usr/local/bin/libra

# Declare that the application listens on port 8080
# and that this port should be exposed
EXPOSE 8080

# Declare that the container uses a volume
# for the /uploads directory
VOLUME /uploads

# Create an unprivileged user to run the application
RUN adduser -H -S -s /dev/null libra

# Switch to that user
USER libra

# Configure the executable as the process to launch
# when the container starts
CMD ["/usr/local/bin/libra"]
