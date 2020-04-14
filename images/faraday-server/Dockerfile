FROM ubuntu:18.04

# Install required tools for faraday download
RUN apt update && apt install -y git

# Close faraday git repository
WORKDIR /
RUN git clone https://github.com/infobyte/faraday.git

# Checkout a stable release version
WORKDIR /faraday
RUN git checkout tags/v3.10.2 -b v3.10.2

# Install the server's system dependencies
RUN apt install -y python3.6 build-essential ipython3 \
    python3-setuptools python3-pip python3.6-dev \
    libssl-dev libffi-dev pkg-config libssl-dev \
    libffi-dev libxml2-dev libxslt1-dev libfreetype6-dev \
    libpng-dev libpq-dev

# Install the server's python dependencies
RUN pip install -U -r requirements_server.txt

# Apply default configuration files
RUN mkdir -p /root/.faraday/config && \
    cp /faraday/config/default.xml /root/.faraday/config/config.xml && \
    cp /faraday/server/default.ini /root/.faraday/config/server.ini

COPY ./run-faraday-server.py /run-faraday-server.py

CMD python /run-faraday-server.py \
    --faraday-root /root/faraday \
    --faraday-data /root/.faraday
