FROM node:22-bookworm AS node

FROM python:3.12-slim

# Bring in Node.js and npm from the Node image
COPY --from=node /usr/local /usr/local
ENV PATH="/usr/local/bin:${PATH}"

RUN apt-get update \
  && apt-get install -y build-essential git \
  && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Copy chatkit backend + frontend and your engine package from the monorepo
COPY chatkit-starter-app/chatkit/package*.json ./
COPY chatkit-starter-app/chatkit/backend ./backend
COPY chatkit-starter-app/chatkit/frontend ./frontend

# Install Python deps (engine + backend) and JS deps
RUN pip install -e ./backend \
  && npm install \
  && cd frontend && npm install && cd ..

EXPOSE 3000

# Run both backend and frontend via the existing npm scripts
CMD ["npm", "run", "dev"]
