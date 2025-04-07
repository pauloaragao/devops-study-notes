FROM node:22.14.0

# Set the working directory
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . .

# Execute npm install to install the dependencies
RUN npm install

# Initialize the application
ENTRYPOINT ["node", "server.js"]

# Expose the port
EXPOSE 8080