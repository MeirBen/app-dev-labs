### STAGE 1: Build ###
FROM registry.access.redhat.com/ubi8/nodejs-18 AS build
RUN mkdir -p /tmp/ngapp
WORKDIR /tmp/ngapp
COPY ./ngapp/package.json ./
RUN npm install
COPY ./ngapp .
RUN npm run build

### STAGE 2: Run ###
FROM registry.access.redhat.com/ubi8/nginx-120:latest
COPY nginx.conf /etc/nginx/nginx.conf
COPY --from=build /tmp/ngapp/dist/ngapp /usr/share/nginx/html
EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]