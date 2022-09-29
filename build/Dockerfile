FROM python:3.10-alpine3.16
LABEL maintainer="joshbright.com"

ENV PYTHONUNBUFFERED 1

COPY ./requirements.txt /tmp/requirements.txt
COPY ./requirements.dev.txt /tmp/requirements.dev.txt
COPY ../app /app
WORKDIR /app
EXPOSE 8000


# Setup a default dev value
# this gets set to true in the docker compose file
ARG DEV=false

# This all runs with one RUN command
# So that it treats this all as one layer
RUN python -m venv /py && \
    /py/bin/pip install --upgrade pip && \
    /py/bin/pip install -r /tmp/requirements.txt && \
    if [ $DEV = "true" ]; \
        then /py/bin/pip install -r /tmp/requirements.dev.txt ; \
    fi && \
    rm -rf /tmp && \
    adduser \
        --disabled-password \
        --no-create-home \
        django-user

ENV PATH="/py/bin:$PATH"

# ensure we aren't using the root user
USER django-user
