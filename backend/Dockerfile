FROM node:16-alpine3.17
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .

ENV MONGODB_URI mongodb://database/yolomy
EXPOSE 5000
ENTRYPOINT ["npm","start"]