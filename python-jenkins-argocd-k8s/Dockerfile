FROM python:3.11-slim

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

# Copy requirements first to leverage docker cache if you have requirements.txt
COPY requirements.txt /app/requirements.txt
RUN pip install --no-cache-dir -r /app/requirements.txt

# Copy project
COPY . /app

# Use an entrypoint to run migrations at runtime (not at build)
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
CMD ["gunicorn", "yourproject.wsgi:application", "--bind", "0.0.0.0:8000"]
