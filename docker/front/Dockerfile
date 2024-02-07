# Use an official Node.js runtime as a parent image
FROM node:14

COPY ./src/dondake /var/www/html

WORKDIR /var/www/html

RUN npm install

# Make port 8080 available to the world outside this container
EXPOSE 8080

# Define environment variable
ARG NODE_ENV=development
ENV NODE_ENV=${NODE_ENV}

# Run npm start when the container launches
CMD ["npm", "run", "dev"]