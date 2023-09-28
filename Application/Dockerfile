# FROM registry.access.redhat.com/ubi8/nodejs-16

# # Create app directory
# WORKDIR /tmp

# USER root
# # copy packge.json to the workdir
# COPY src/package*.json ./


# # install npm dependencies
# RUN npm install && npm audit fix --force

# # Copy application file to the 
# COPY src .

# # create local env varibel for the PORT
# ENV PORT 8080

# USER 1001

# EXPOSE 8080
# CMD [ "node", "app.js" ]

# Stage 1: Build the Angular application
FROM registry.access.redhat.com/ubi8/nodejs-16
WORKDIR /tmp/ng
COPY package.json package-lock.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2: Serve the Angular application using Nginx
FROM nginx:alpine
COPY --from=build /app/dist/your-angular-app-name /usr/share/nginx/html
COPY ./nginx-custom.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
