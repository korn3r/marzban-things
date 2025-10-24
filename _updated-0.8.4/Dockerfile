ARG PYTHON_VERSION=3.12

FROM python:$PYTHON_VERSION-alpine3.21 AS build

ENV PYTHONUNBUFFERED=1

WORKDIR /code

RUN apk add --update --no-cache curl unzip py3-pip build-base python3-dev libpq-dev linux-headers
RUN pip install --no-cache-dir --upgrade pip
RUN curl -L https://github.com/Gozargah/Marzban-scripts/raw/master/install_latest_xray.sh | sh

COPY ./requirements.txt /code/
RUN pip install --upgrade pip setuptools \
    && pip install --no-cache-dir --upgrade -r /code/requirements.txt

RUN rm -rf /var/cache/apk/*

FROM python:$PYTHON_VERSION-alpine3.21

ENV PYTHON_LIB_PATH=/usr/local/lib/python${PYTHON_VERSION%.*}/site-packages
WORKDIR /code

RUN rm -rf $PYTHON_LIB_PATH/*
RUN apk add --update --no-cache bash
RUN apk add --no-cache --upgrade

COPY --from=build $PYTHON_LIB_PATH $PYTHON_LIB_PATH
COPY --from=build /usr/local/bin /usr/local/bin
COPY --from=build /usr/local/share/xray /usr/local/share/xray

COPY . /code

RUN ln -s /code/marzban-cli.py /usr/bin/marzban-cli
RUN chmod +x /usr/bin/marzban-cli
RUN marzban-cli completion install --shell bash

CMD ["bash", "-c", "alembic upgrade head; python main.py"]
