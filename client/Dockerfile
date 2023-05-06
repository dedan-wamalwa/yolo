FROM node:16-alpine3.17
WORKDIR /app
COPY package.json . 
RUN npm install
COPY . .
RUN npm test
RUN npm run build

EXPOSE $PORT
ENTRYPOINT ["npm","start"]

