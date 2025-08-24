# Etapa de build
FROM node:15 AS builder

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

RUN npm run build

# Etapa de produção (usa imagem leve do nginx ou serve com node)
FROM nginx:alpine

# Copia os artefatos de build para o nginx
COPY --from=builder /app/build /usr/share/nginx/html

# Expõe porta 8080 (pra bater com o exercício)
EXPOSE 8080

# Substitui a config default do nginx para ouvir na 8080
RUN sed -i 's/80/8080/g' /etc/nginx/conf.d/default.conf

CMD ["nginx", "-g", "daemon off;"]
