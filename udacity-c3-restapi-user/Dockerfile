FROM node:13

# Set app directory
WORKDIR /usr/src/app

# Install app dependencies
COPY package*.json ./
RUN npm ci

# Run application
COPY . .
EXPOSE 8080
CMD [ "npm", "run", "prod" ]