FROM node:lts-alpine

WORKDIR /usr/src/app

# Copia só os manifests primeiro (melhor aproveitamento de cache)
COPY package*.json ./

RUN npm install

# Copia o restante do código
COPY . .

EXPOSE 3000

CMD ["npm", "run", "start:dev"]
