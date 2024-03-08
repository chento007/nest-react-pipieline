FROM node:16.10.0-alpine

WORKDIR /app

# Set the environment variable
ENV NODE_ENV=development

# Copy package.json and package-lock.json
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose the port the app runs on
EXPOSE 3000

# Correct start command for development environment
CMD ["npm", "run", "dev"]
