FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt --no-cache-dir

COPY . .

RUN python manage.py collectstatic --no-input

CMD ["gunicorn", "--bind", "0.0.0.0:9090", "kittygram_backend.wsgi"]
