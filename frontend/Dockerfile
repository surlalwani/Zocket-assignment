# Use an official Node.js runtime as a base image
FROM node:14-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy the package.json and package-lock.json files to the container
COPY package*.json ./

# Install the dependencies
RUN npm install

# Copy the rest of the application code to the container
COPY . .

# Build the React application for production
RUN npm run build

# Use a lightweight Nginx server as a base image for serving the production build
FROM nginx:alpine

# Copy the built React application from the previous stage to the Nginx server
COPY --from=0 /app/build /usr/share/nginx/html

# Expose the port on which the Nginx server will listen (default is 80)
EXPOSE 80

# Start the Nginx server
CMD ["nginx", "-g", "daemon off;"]
