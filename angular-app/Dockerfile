FROM node:12.16-alpine3.9
RUN mkdir -p /app
WORKDIR /app
COPY package.json /app/
RUN npm install
RUN npm install -g @angular/cli
COPY . /app/
EXPOSE 4200
CMD ["npm", "start"]
