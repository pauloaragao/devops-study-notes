FROM node:20.9.0-alpine3.18

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json .

# Install the dependencies
RUN npm install

# Copy the current directory contents into the container at /app
COPY . .

# Initialize the application
ENTRYPOINT ["node", "server.js"]

# Expose the port
EXPOSE 8080