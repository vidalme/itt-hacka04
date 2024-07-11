# Etapa de construção
FROM node:16 AS build

# Diretório de trabalho
WORKDIR /app

# Copiar arquivos de configuração e instalar dependências
COPY package*.json ./
RUN npm install

# configin to accept buildtime env vars
ARG VITE_BASE_BACKEND_URL
ENV VITE_BASE_BACKEND_URL=$VITE_BASE_BACKEND_URL

# Copiar o restante dos arquivos do projeto e construir o frontend
COPY . .
RUN npm run build


# Etapa de produção
FROM nginx:alpine

# Copiar o build da etapa anterior
COPY --from=build /app/dist /usr/share/nginx/html

# Copiar a configuração do Nginx
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expor a porta 80
EXPOSE 80

# Comando para iniciar o Nginx
CMD ["nginx", "-g", "daemon off;"]

