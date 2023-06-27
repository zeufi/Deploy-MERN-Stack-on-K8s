# Stage 1: Build the React app
FROM node:14-alpine AS todo-app-build
WORKDIR /client

# Clear yarn cache
RUN yarn cache clean

COPY package.json yarn.lock README.md ./
RUN yarn install

COPY ./public ./public
COPY ./src ./src
ENV REACT_APP_baseAPIURL=http://192.168.58.2:32328

# Upgrade npm
RUN npm install -g npm

# Build the app
RUN yarn build

# Stage 2: Serve the app using Nginx
FROM nginx:latest
LABEL maintainer=Aamir-Pinger

COPY --from=todo-app-build /client/build/ /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
