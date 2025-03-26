FROM node:18-alpine AS build
WORKDIR /usr/src/app
COPY package*.json ./
COPY . .
RUN npm ci --force  \
    &&  npm run build

#RELEASE STAGE

FROM nginx:1.23.1-alpine AS release
EXPOSE 80
COPY --from=build /usr/src/app/dist /usr/share/nginx/html
COPY nginx/nginx.conf /etc/nginx/nginx.conf
CMD ["nginx", "-g", "daemon off;"]