FROM node:18-alpine as build

# Рабочая директория внутри контейнера
WORKDIR /app

# Копируем файлы с зависимостями (package.json и package-lock.json)
COPY package*.json ./
RUN npm ci

# Копируем ВЕСЬ код фронтенда
COPY . .

# Собираем React приложение в статические файлы
RUN npm run build

# Легкий образ для хранения статических файлов
FROM alpine:latest

# Копируем собранные статические файлы из предыдущего этапа
# --from=build - берем из предыдущего образа (этап build)
COPY --from=build /app/build /static

# Команда, которая держит контейнер запущенным
# Без этого контейнер сразу завершится, а volume не передастся
CMD ["sh", "-c", "echo 'Frontend built successfully' && tail -f /dev/null"]