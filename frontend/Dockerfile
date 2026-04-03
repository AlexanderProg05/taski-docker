FROM node:18 as build
WORKDIR /app

# Копируем файлы зависимостей
COPY package.json package-lock.json ./

# Очищаем кэш npm и устанавливаем зависимости с увеличенным таймаутом
RUN npm cache clean --force && \
    npm install --no-audit --no-fund --loglevel=error --fetch-retries=5 --fetch-retry-mintimeout=20 --fetch-retry-maxtimeout=120

# Копируем остальной код
COPY . .

# Принудительно устанавливаем react-scripts, если вдруг его нет (на всякий случай)
RUN npm install react-scripts --save --no-audit

# Сборка приложения
RUN npm run build

# Финальный образ: только статика
FROM alpine:latest
WORKDIR /static
COPY --from=build /app/build /static/build
