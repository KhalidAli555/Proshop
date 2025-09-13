# Use Node.js base image
FROM node:18

# Set working directory inside container
WORKDIR /app

# Copy package.json & package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy rest of backend code
COPY . .

# Expose backend port
EXPOSE 5000

# Run backend server
CMD ["npm", "run", "server"]
