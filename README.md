# Bhojan Prototype 2 Frontend: 

This project is based on ReactJS in frontend, [NodeJS in backend](https://github.com/bug-tracker-software/bts-be-prototype-2) and MongoDB as a database.

It contains complete authentication and user management system.


Material UI Examples

https://github.com/mui/material-ui/blob/master/docs/data/material/getting-started/templates/pricing/Pricing.js

Internationalizing and Localizing:
https://www.youtube.com/watch?v=baLjPx_wFi4

JSON Translator:
https://translate.i18next.com/

Deployment:
https://www.youtube.com/watch?v=eKEiKbPaFJg&t=477s


Create .env or .env.local

REACT_APP_ENV="Development"
REACT_APP_ENABLE_DEBUG=true
REACT_APP_BACKEND_LINK="http://localhost:3001"
REACT_APP_STRIPE_PUBLISHABLE_KEY="XXXX"

## DOCKER-COMPOSE.YAML

```
version: '3.8'
services: 
  db:
    image: mongo
    container_name: mongo
    ports:
      - '27017:27017'
    networks:
      - bhojan-network
    volumes:
      - ./data:/data/db
  backend:
    build: ./bhojan-be-prototype-2
    container_name: backend
    ports:
      - '3001:3001'
    env_file:
      - ./bhojan-be-prototype-2/.env.docker
    networks:
      - bhojan-network
    depends_on:
      - db
  frontend:
    build: ./bhojan-fe-prototype-2
    container_name: frontend
    ports:
      - '3000:3000'
    env_file:
      - ./bhojan-fe-prototype-2/.env.docker
    networks:
      - bhojan-network
    stdin_open: true
    tty: true
    depends_on:
      - backend
networks:
  bhojan-network:
    driver: bridge
```