# Use the official Node.js image as base
FROM node:latest

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy the rest of the application code to the working directory
COPY ../ /usr/src/app

# Expose the port the app runs on
EXPOSE 9997

# Command to run the application
CMD node app.js ./splitter