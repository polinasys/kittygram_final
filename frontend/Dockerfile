FROM node:18-alpine as build

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build

FROM alpine:latest
COPY --from=build /app/build /static

CMD ["sh", "-c", "echo 'Frontend built successfully' && tail -f /dev/null"]