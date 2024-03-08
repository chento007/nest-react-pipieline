FROM node:16.18.1 as builder

WORKDIR /app

COPY package*.json ./

RUN npm i

COPY . .

RUN npm run build

FROM nginx:latest

COPY --from=builder /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
