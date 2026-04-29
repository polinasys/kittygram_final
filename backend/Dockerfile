FROM python:3.9-slim

WORKDIR /app

RUN apt-get update && apt-get install -y \
    gcc \
    libpq-dev \
    libjpeg-dev \
    zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .

RUN pip install -r requirements.txt --no-cache-dir

COPY . .

# Создаем директорию для статики
RUN mkdir -p /staticfiles

RUN python manage.py collectstatic --no-input

CMD ["gunicorn", "--bind", "0.0.0.0:9090", "kittygram_backend.wsgi"]