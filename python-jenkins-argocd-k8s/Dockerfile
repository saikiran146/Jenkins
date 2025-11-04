FROM python:3

# Prevent Python buffering issues
ENV PYTHONUNBUFFERED=1

# Install system deps (including distutils) and cleanup
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
      python3-distutils \
      build-essential \
      gcc \
      libssl-dev \
      # add any DB client dev libs you need (example for postgres):
      # libpq-dev \
    && rm -rf /var/lib/apt/lists/*

# Copy project files and install python deps
WORKDIR /app
COPY . /app

# Install pip requirements if you have a requirements.txt
# RUN pip install --no-cache-dir -r requirements.txt

# Run migrations (or run them from entrypoint/CI)
RUN python manage.py migrate

# Expose / CMD as needed
# EXPOSE 8000
# CMD ["gunicorn", "yourproject.wsgi:application", "--bind", "0.0.0.0:8000"]
