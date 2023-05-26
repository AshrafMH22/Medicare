FROM node:16

# RUN mkdir -p /app

WORKDIR /usr/src/app

COPY . .

RUN npm install -g @angular/cli

RUN npm install

RUN ng test

RUN ng serve -o

EXPOSE 4200

