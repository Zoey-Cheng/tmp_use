# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set metadata indicating the maintainer of the image
LABEL maintainer="Ziyun Cheng <zc3068@nyu.edu>"

# Set environment variables to reduce Python package issues and ensure output is sent straight to the terminal without buffering
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Install system dependencies required for Python packages
RUN apt-get update && \
    apt-get install -y gcc libc-dev && \
    # Clean up the apt cache to reduce image size
    rm -rf /var/lib/apt/lists/* \
    build-essential

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
