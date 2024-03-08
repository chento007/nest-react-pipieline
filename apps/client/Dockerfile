FROM node:18-alpine

# Set the working directory in the container
WORKDIR /app

# Copy the package.json file to install dependencies
COPY package.json .

# Install dependencies, including vite
RUN npm install

# Copy the rest of your app's source code
COPY . .

# Ensure everything in the app directory is owned by the non-root user 'node'
# and ensure executables in node_modules can be executed
RUN chown -R node:node /app && chmod -R 755 /app/node_modules

# Use the non-root user to run your application
USER node

# Your application listens on port 8080, so expose it
EXPOSE 8080

# Define the command to run your application
CMD [ "npm", "run", "dev" ]
