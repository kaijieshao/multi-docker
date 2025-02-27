FROM node:16-alpine as builder
WORKDIR '/app'
COPY ./package.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx
# Starts a new build stage using the official Nginx image as the base
# This creates a much smaller final image by discarding the Node.js build environment

EXPOSE 3000
# Informs Docker that the container will listen on port 3000 at runtime

COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
# Copies a custom Nginx configuration file from the host to the appropriate location in the Nginx container

COPY --from=builder /app/build /usr/share/nginx/html
# Copies only the build artifacts from the previous "builder" stage to the Nginx html directory
# This is where Nginx will serve static files from
