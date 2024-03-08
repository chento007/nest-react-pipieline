# Stage 1: Build the React application
FROM node:16.18.1 AS builder

WORKDIR /app

COPY package*.json ./
COPY yarn.lock ./

# Install dependencies
RUN npm install
# OR
# RUN yarn install

COPY . .

RUN npm run build
# OR
# RUN yarn build

# Stage 2: Serve the app with Nginx
FROM nginx:alpine

COPY --from=builder /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
