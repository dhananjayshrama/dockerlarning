# Docker Learning – Level 1

A small Node.js (Express) app containerized with Docker. I built it while learning Docker from YouTube tutorials and practicing the core concepts hands-on.

## Tech Stack
Node.js, Express 5, dotenv, Docker

## Project Structure
```
.
├── Dockerfile
├── .dockerignore
├── index.js
├── package.json
└── package-lock.json
```

## Run Locally
```bash
npm install
npm start
```

## Run with Docker
```bash
docker build -t docker-learning .
docker run -p 5000:5000 docker-learning
```
Open http://localhost:5000. You should see:
```json
{ "message": "hello from docker 27" }
```

## Dockerfile
```dockerfile
FROM node:22-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
EXPOSE 5000
CMD ["node", "index.js"]
```

## What I Learned
- Image vs container: an image is the blueprint, a container is a running instance
- Dockerfile instructions: `FROM`, `WORKDIR`, `COPY`, `RUN`, `CMD`, `EXPOSE`
- Layer caching: copying `package*.json` before the source code avoids reinstalling dependencies on every change
- `RUN` runs at build time, `CMD` runs when the container starts
- `.dockerignore` keeps `node_modules` and other unneeded files out of the image
- Port mapping with `-p hostPort:containerPort`
- Configuring the app with environment variables (`docker run -e PORT=8000 ...`)

## Next Steps
- Run as a non-root user
- Docker Compose
- Multi-stage builds

## Learning Source
Learned from YouTube tutorials, then built and tested this project on my own.
