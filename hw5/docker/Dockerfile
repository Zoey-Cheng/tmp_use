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

# Set the working directory in the container
WORKDIR /hw5

# Copy the Python requirements file into the container at /hw4
COPY mnist/requirements.txt /hw5/requirements.txt

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r /hw5/requirements.txt

# Copy the rest of the application
COPY mnist/main.py /hw5/main.py

# Make port 8000 available to the world outside this container
EXPOSE 8000

# Run main.py when the container launches
CMD [ "python3", "train.py", "--epochs=1", "--save-model" ]
