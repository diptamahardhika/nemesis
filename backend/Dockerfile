FROM node:20-slim

# Install PM2 globally
RUN npm install pm2 -g

# Set the working directory
WORKDIR /app

# Copy package files
COPY package*.json ./

# Install production dependencies
RUN npm install --omit=dev

# Copy the rest of the application code
COPY . .

# Create data directory (where the SQLite DB is expected) 
# and ensure the node user has permissions
RUN mkdir -p data && chown -R node:node /app

# Switch to non-root user for security
USER node

# Expose port 3000
EXPOSE 3000

# Start the application using PM2
# pm2-runtime ensures the application restarts on exceptions and handles Docker signals correctly
CMD ["pm2-runtime", "src/server.js"]
