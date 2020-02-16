## Build
FROM beevelop/ionic as ionic

# Set app directory
WORKDIR /usr/src/app

# Install app dependencies
COPY package*.json ./
RUN npm ci

# Build app
COPY . .
RUN ionic build

## Run
FROM nginx:alpine
COPY --from=ionic /usr/src/app/www /usr/share/nginx/html