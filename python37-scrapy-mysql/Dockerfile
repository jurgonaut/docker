# Create a compile image and install all dependencies
FROM debian:stable-slim AS compile-image

# Install dependencies
RUN apt-get update && \
    apt-get install --no-install-recommends -y gcc python3 python3-setuptools python3-pip python3-dev default-libmysqlclient-dev

# Install requirements in root 
COPY requirements.txt .
RUN pip3 install --user -r requirements.txt

# Create a build image
FROM debian:stable-slim AS build-image

# Copy over the packages
COPY --from=compile-image /root/.local /root/.local

# Install the needed dependencies (default-libmysqlclient-dev)
RUN apt-get update && \
    apt-get install --no-install-recommends -y python3 default-libmysqlclient-dev && \
    apt autoremove --purge && \
    apt-get autoclean && \
    rm -rf /var/cache/apt

# Make sure scripts in .local are usable:
ENV PATH=/root/.local/bin:$PATH

COPY test.py .

# NOTE: the Dockerfile generates intermidiate images (multi-stage build) to remove them
# run 'echo "y" | docker system prune' (note that this command can remove other things too so be careful)