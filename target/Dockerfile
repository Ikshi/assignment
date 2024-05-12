# Use the official Node.js image as base
FROM node:latest

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json to the working directory
#COPY package-lock.json ./

# Install app dependencies
#RUN npm install

# Copy the rest of the application code to the working directory
#COPY ../app.js /usr/src/app
COPY ../ /usr/src/app

# Expose the port your app runs on
EXPOSE 9997

# Command to run the application
CMD node app.js ./target