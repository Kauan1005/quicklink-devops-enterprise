# ESTÁGIO 1: Builder
FROM node:18-alpine AS builder
WORKDIR /app

# Criando o package.json
RUN echo '{"name": "quicklink","version": "1.0.0","scripts": {"build": "echo build-concluido"}}' > package.json

# Criando a pasta dist e o arquivo html (Comandos separados)
RUN mkdir dist
RUN echo '<h1>QuickLink funcionando via Nginx e Docker!</h1>' > dist/index.html

# Executando o build fake
RUN npm run build

# ESTÁGIO 2: Production
FROM nginx:alpine AS production
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx/nginx.conf /etc/nginx/conf.d/
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]