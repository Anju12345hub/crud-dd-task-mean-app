# Stage 1: Build Angular App
FROM node:lts-alpine as builder

WORKDIR /app
COPY package.json package-lock.json ./
RUN npm install

COPY . .
RUN npm run build --prod

# Stage 2: Serve Angular with Nginx
FROM nginx:alpine

# Replace '/app/dist/<project-name>' with your Angular project name from angular.json
COPY --from=builder /app/dist/angular-15-crud /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

