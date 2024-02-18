FROM node:19-alpine AS build

WORKDIR /app
COPY package.json ./
COPY package-lock.json ./
RUN npm install
COPY . .

RUN npm run build

FROM nginx:alpine AS production
COPY --from=build /app/dist/ /usr/share/nginx/html

EXPOSE 3000

# Start Nginx and keep it running in the foreground
CMD ["nginx", "-g", "daemon off;"]
