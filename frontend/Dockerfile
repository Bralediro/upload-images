# Name the node stage "build-stage"
FROM node:12.18.3-alpine3.9 as build-stage
# Set working directory
WORKDIR /app
COPY package*.json ./
RUN npm install
# Copy all files from current directory to working dir in image
COPY . .
RUN npm run build

# nginx state for serving content
FROM nginx:1.18.0-alpine as production-stage
# Copy static assets from builder stage
COPY --from=build-stage /app/dist /usr/share/nginx/html
EXPOSE 80
# Containers run nginx with global directives and daemon off
CMD ["nginx", "-g", "daemon off;"]





