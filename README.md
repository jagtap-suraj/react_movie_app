# React Movie App

A React application for browsing movies using the OMDB API.

## Docker Setup

### Prerequisites
- Docker and Docker Compose installed on your machine

### Building and Running with Docker

1. **Build and start the container:**
   ```bash
   docker-compose up -d --build
   ```

2. **Access the application:**
   Open your browser and navigate to: http://localhost:3001

3. **Stop the container:**
   ```bash
   docker-compose down
   ```

### Development with Docker

For development with hot reload, you can modify the docker-compose.yml file to:
```yaml
version: '3.8'

services:
  app:
    build:
      context: .
      dockerfile: Dockerfile.dev
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=development
      - REACT_APP_OMDB_API_KEY=${REACT_APP_OMDB_API_KEY}
    volumes:
      - ./src:/app/src
      - ./public:/app/public
    restart: unless-stopped
```

And create a Dockerfile.dev with:
```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package.json package-lock.json* ./
RUN npm install

COPY . .

EXPOSE 3000
CMD ["npm", "start"]
```

### Setup API

1. Go to the [OMDb API](https://www.omdbapi.com/apikey.aspx) and request an API key.
2. Add your details, get your API key and activate it.
3. Create a file called `.env` in the root of the project.
4. Add the following to the `.env` file:
   `REACT_APP_OMDB_API_KEY=your_api_key`
5. Replace `your_api_key` with the API key you got from the OMDb API.
6. run `npm install` to install all dependencies.
7. run `npm start` to start the application.
8. Go to `http://localhost:3000` to view the application.
