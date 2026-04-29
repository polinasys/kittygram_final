FROM python:3.9-slim

# Устанавливаем рабочую директорию внутри контейнера
# Все дальнейшие команды будут выполняться из этой папки
WORKDIR /app

# Копируем файл с зависимостями из хоста в контейнер
COPY requirements.txt .

# Устанавливаем зависимости Python внутри контейнера
# --no-cache-dir: не сохранять кэш pip, чтобы уменьшить размер образа
RUN pip install -r requirements.txt --no-cache-dir

# Копируем ВЕСЬ код бэкенда из хоста в контейнер
COPY . .

# Собираем статические файлы Django (CSS, JS, изображения админки)
# --no-input: не запрашивать подтверждение у пользователя
RUN python manage.py collectstatic --no-input

# Команда для запуска контейнера
CMD ["gunicorn", "--bind", "0.0.0.0:9090", "kittygram_backend.wsgi"]
