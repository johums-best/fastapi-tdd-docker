# pull official base image
FROM python:3.11.2-slim-buster

# set working directory
RUN mkdir -p /usr/src/code
WORKDIR /usr/src/code

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# install system dependencies
RUN apt-get update \
  && apt-get -y install netcat gcc \
  && apt-get clean

# install python dependencies
RUN pip config set global.index-url https://pypi.douban.com/simple
RUN pip install --upgrade pip
COPY ./requirements.txt .
RUN pip install -r requirements.txt

# ENV PYTHONPATH=/usr/src/code:$PYTHONPATH

# add code
COPY . .

# add entrypoint.sh
COPY ./entrypoint.sh .
RUN chmod +x /usr/src/code/entrypoint.sh

# run entrypoint.sh
ENTRYPOINT ["/usr/src/code/entrypoint.sh"]