# Docker_Learning
I will all the notes and code examples here, 


## Multi-Stage Build

To optimize the image and improve the build process, you can use multi-stage builds in Docker. 

A multi-stage build involves creating multiple build stages in a single Dockerfile. Each stage can have its own set of instructions and dependencies. The final image is built from the last stage, but the intermediate stages are discarded, resulting in a smaller and more efficient image.

Here's an example of a multi-stage build in a Dockerfile:

```Dockerfile
# Stage 1: Build the application
FROM node:14 as builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2: Create the production image
FROM nginx:alpine
COPY --from=builder /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]