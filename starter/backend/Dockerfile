FROM python:3.10-slim-bookworm

ENV FLASK_RUN_HOST=0.0.0.0

WORKDIR /app

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential \
    libpcre3 \
    libpcre3-dev \
    && rm -rf /var/lib/apt/lists/*

RUN pip install --no-cache-dir pipenv==2023.2.4

COPY Pipfile Pipfile.lock ./

RUN pipenv sync --system

COPY . .

EXPOSE 5000

CMD ["uwsgi", "--http", ":5000", "--master", "--enable-threads", "--manage-script-name", "--mount", "/=app:app"]