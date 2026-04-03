FROM node:18 as build
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm cache clean --force && \
    npm install --no-audit --no-fund --loglevel=error --fetch-retries=5 --fetch-retry-mintimeout=20 --fetch-retry-maxtimeout=120
COPY . .
RUN npm install react-scripts --save --no-audit
RUN npm run build
FROM alpine:latest
WORKDIR /static
COPY --from=build /app/build /static/build
