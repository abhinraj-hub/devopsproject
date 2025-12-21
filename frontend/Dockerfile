FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm install --legacy-peer-deps
RUN npm uninstall @types/node
RUN npm install --save-dev @types/node@18.19.50 --legacy-peer-deps
COPY . .
RUN npm run build -- --configuration production
FROM nginx:alpine
COPY --from=build /app/dist/angular-15-crud /usr/share/nginx/html/
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
