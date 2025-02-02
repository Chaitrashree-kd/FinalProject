# Use a Node.js base image
FROM node:14

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json (if present)
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the frontend files
COPY . .

# Build the frontend (add this part if you're using a framework like React)
RUN npm run build

# Install a web server (e.g., serve) to serve the build files
RUN npm install -g serve

# Serve the built application
CMD ["serve", "-s", "build", "-l", "5000"]

# Expose port 5000 for the frontend
EXPOSE 5000
