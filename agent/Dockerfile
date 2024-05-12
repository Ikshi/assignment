# Use the official Node.js image as base
FROM node:latest

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install app dependencies
#RUN npm install

# Copy the rest of the application code to the working directory
COPY ../ /usr/src/app

# Expose the port your app runs on
EXPOSE 3000

# Command to run the application
CMD node app.js ./agent