# Start with a Linux micro-container to keep the image tiny
FROM python:3.8-slim

# Document who is responsible for this image
LABEL maintainer="Ziyun Cheng <zc3068@nyu.edu>"

# Install just the Python runtime (no dev)
# Install just the Python runtime and other necessary packages
RUN apt-get update && \
    apt-get install -y gcc libc-dev && \
    rm -rf /var/lib/apt/lists/*

# Set up a working folder and install the pre-reqs
WORKDIR /app
ADD src/requirements.txt /app/requirements.txt
RUN pip3 install --upgrade pip setuptools
RUN pip3 install --no-cache-dir -r /app/requirements.txt

# Add the code as the last Docker layer because it changes the most
ADD src/inference.py  /app/inference.py
ADD src/main.py  /app/main.py

# Run the service
WORKDIR /app
EXPOSE 5000
CMD [ "python3", "main.py"]
