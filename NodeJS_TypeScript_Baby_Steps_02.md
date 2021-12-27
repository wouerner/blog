# NodeJS TypeScript: Baby Steps #02 - Nodemon + ts-node 

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
git clone --depth 1 --branch v1.0.1 git@github.com:wouerner/nodejs-typescript.git
```
---
install express:
```
docker-compose run app npm install express 
```

---

install typescript definitions for node:
```
docker-compose run app npm install -D @types/node
```

---
install typescript definitions for **express**:
``` sh
docker-compose run app npm install -D @types/express 
```
---

install typescript definitions for **express**:
```
nvim index.ts 
```
``` javascript
import express, {Request,Response,Application} from 'express';

const app:Application = express();

const PORT = process.env.PORT || 8000;

app.get("/", (req:Request, res:Response):void => {
  res.send("Hello Typescript with Node.js!")
});

app.listen(PORT, ():void => {
  console.log(`Server Running here 👉 https://localhost:${PORT}`);
});
```
 
---
install nodemon definitions:
```
docker-compose run app npm install -D nodemon
```
---
add the definitions:
```
nvim package.json
```

---

install ts-node definitions:
```
docker-compose run app npm install -D ts-node
```
---
run the project
``` sh
docker-compose up build 
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
# CMD [ "npm", "run", "start-dev" ]
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
  app:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: nodejs-typescript
    volumes:
      - ./:/app
      - /app/node_modules
    ports:
      - "3000:3000"

  db:
    image: 'mongo'
    container_name: typescript-mongodb
    ports:
      - '27017:27017'
    volumes:
      - /data/db
```

---

The end

---
## Index
