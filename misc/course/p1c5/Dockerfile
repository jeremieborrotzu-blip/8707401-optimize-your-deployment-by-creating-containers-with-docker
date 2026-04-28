FROM ubuntu:noble

# Make the Libra application version to download configurable,
# along with the integrity checksum of the desired archive
ARG LIBRA_VERSION=0.0.1
ARG LIBRA_CHECKSUM=d0757c5b427825126f98ffa07683d676fb8c62a02d098659cce9d3cd485b79a0
ARG LIBRA_REPOSITORY=https://github.com/Bornholm/libra

# Update system dependencies to reduce the risk
# of security vulnerabilities in the final image
RUN apt-get update -y && DEBIAN_FRONTEND=noninteractive apt-get upgrade -y

# Install the dependencies required to download the Libra application
RUN apt-get update -y && DEBIAN_FRONTEND=noninteractive apt-get install -y wget

# Download the archive containing the Libra executable
RUN wget \
    -O libra.tar.gz \
    ${LIBRA_REPOSITORY}/releases/download/v${LIBRA_VERSION}/libra_${LIBRA_VERSION}_linux_amd64.tar.gz

# Verify the archive checksum
RUN echo "${LIBRA_CHECKSUM} libra.tar.gz" | sha256sum --check --status

# Create the /usr/local/bin directory
RUN mkdir -p /usr/local/bin

# Extract the Libra binary from the archive
# and place it directly in the /usr/local/bin directory
RUN tar -xzf libra.tar.gz -C /usr/local/bin libra

# Ensure the binary is executable
RUN chmod +x /usr/local/bin/libra

# Declare that the application listens on port 8080
# and that this port should be exposed
EXPOSE 8080

# Declare that the container uses a volume
# for the /uploads directory
VOLUME /uploads

# Configure the executable as the process to launch
# when the container starts
CMD ["/usr/local/bin/libra"]
