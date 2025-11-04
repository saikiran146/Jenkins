FROM python:3.10-slim

ENV PYTHONUNBUFFERED=1
WORKDIR /app

# Install OS deps including distutils (available on this image)
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
      python3-distutils \
      build-essential \
      gcc \
      libssl-dev \
      libpq-dev \
    && rm -rf /var/lib/apt/lists/*

# Install pip deps (assumes requirements.txt exists)
COPY requirements.txt /app/requirements.txt
RUN pip install --no-cache-dir -r /app/requirements.txt

# Copy project
COPY . /app

# Migrations at container start (recommended) - entrypoint below
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
CMD ["gunicorn", "yourproject.wsgi:application", "--bind", "0.0.0.0:8000"]
