FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install --production

COPY app/ ./app/

EXPOSE 5000

CMD ["node", "app/index.js"]
