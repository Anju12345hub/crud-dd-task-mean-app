# Stage 1: Build Angular App
FROM node:18 AS build

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build --prod

# Stage 2: Serve with Nginx
FROM nginx:1.25

COPY --from=build /app/dist/frontend /usr/share/nginx/html

# Copy default nginx config (optional)
COPY nginx/reverse-proxy.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
