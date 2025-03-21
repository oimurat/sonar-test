FROM node:22.13.0
ENV NODE_ENV=development

WORKDIR /usr/src/app

COPY react/package.json ./
COPY react/package-lock.json ./
RUN npm install

COPY . .

CMD ["npm", "start"]
