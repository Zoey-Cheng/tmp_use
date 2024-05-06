# Start with a Linux micro-container to keep the image tiny
FROM python:3.8-slim

# Document who is responsible for this image
LABEL maintainer="Ziyun Cheng <zc3068@nyu.edu>"

# Install just the Python runtime (no dev)
RUN apt-get update && apt-get install -y \
    python3 python3-dev gcc gfortran musl-dev \
    python3-pip ca-certificates

# Set up a working folder and install the pre-reqs
WORKDIR /app
ADD src/requirements.txt /app
RUN pip3 install --upgrade pip setuptools
RUN pip3 install -r requirements.txt

# Add the code as the last Docker layer because it changes the most
ADD src/train.py  /app/train.py

# Run the service
WORKDIR /app
EXPOSE 5000
CMD [ "python3", "train.py", "--epochs=1", "--save-model" ]
