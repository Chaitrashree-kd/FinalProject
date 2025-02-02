# Step 1: Use an official Node.js image with Alpine for a smaller footprint
FROM node:14-alpine

# Step 2: Set the working directory inside the container
WORKDIR /app

# Step 3: Copy only the package.json and package-lock.json (if available) to install dependencies first
COPY package.json ./

# Step 4: Install only the production dependencies (excluding devDependencies)
RUN npm install --only=production

# Step 5: Copy the rest of the application files
COPY . .

# Step 6: Expose the application port (make sure your app listens on port 5000)
EXPOSE 5000

# Step 7: Add a non-root user for security reasons (avoiding running the app as root)
RUN adduser -D appuser

# Step 8: Switch to the newly created non-root user for running the app
USER appuser

# Step 9: Specify the command to run the application
CMD ["node", "server.js"]
