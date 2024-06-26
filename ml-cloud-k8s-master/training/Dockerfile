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
    rm -rf /var/lib/apt/lists/*

# Set up a working folder and install the pre-reqs
WORKDIR /app
ADD src/requirements.txt /app
RUN pip3 install --upgrade pip setuptools
RUN pip3 install --no-cache-dir -r requirements.txt

# Install torchvision to use its utilities for downloading MNIST dataset
RUN pip3 install torchvision

# Download the MNIST dataset into the image
RUN python3 -c "from torchvision import datasets, transforms; datasets.MNIST('/app/data', download=True, transform=transforms.ToTensor())"

# Add the code as the last Docker layer because it changes the most
ADD src/train.py  /app/train.py

# Run the service
WORKDIR /app
EXPOSE 5000
CMD [ "python3", "train.py", "--epochs=1", "--save-model" ]
