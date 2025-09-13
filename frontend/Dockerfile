# Stage 1: Build React app
FROM node:18 AS build

WORKDIR /app

# Install dependencies
COPY package*.json ./
RUN npm install

# Copy source code
COPY . .

# Build React app (production build)
RUN npm run build


# Stage 2: Serve static files
FROM node:18-slim

WORKDIR /app

# Install lightweight server
RUN npm install -g serve

# Copy build files from first stage
COPY --from=build /app/build ./build

# Expose frontend port
EXPOSE 3000

# Serve React build
CMD ["serve", "-s", "build", "-l", "3000"]
