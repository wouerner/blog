# NodeJS TypeScript: Baby Steps #01 - Docker

## Requirements
 - docker
 - docker-compose

## Objective
* Configure containers docker to run project.
* initial setup for typescript

## Inspiration:
?

---
Clone the project 

```
git clone git@github.com:wouerner/nodejs-typescript.git
```
---
Create a Dockerfile: 
```
nvim Dockerfile
```
Copy to file:
```
FROM node:16

WORKDIR /app

COPY package*.json ./

RUN npm install --verbose

COPY . .

EXPOSE 3000 
CMD [ "npm", "run", "start-dev" ]
```

---

Create a **docker-compose.yml**: 
```
nvim docker-compose.yml
```
Copy to file:
```
version: '3'

services:
  nodejs-express:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: nodejs-express
    volumes:
      - ./:/app
      - /app/node_modules
    ports:
      - "3000:3000"

  db:
    image: 'mongo'
    container_name: mongodb
    ports:
      - '27017:27017'
    volumes:
      - /data/db
```

---
create a package.json
```
docker-compose run app npm init -y
```
---

install **typescript**
```
docker-compose run app npm i typescript
```
---

create a **tsconfig.json**
```
docker-compose run app npx tsc --init
```

The end

---
## Index

