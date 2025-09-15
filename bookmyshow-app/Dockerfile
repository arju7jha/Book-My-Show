# Use Node.js 18 (or your Jenkins-configured version)
FROM node:18

# Set working directory -----------------
WORKDIR /app

# Copy package.json and package-lock.json
COPY package.json package-lock.json ./

# Install chokidar@3 explicitly (fix for missing dependency)
RUN npm install chokidar@3 --legacy-peer-deps

# Your existing postcss fix
RUN npm install postcss@8.4.21 postcss-safe-parser@6.0.0 --legacy-peer-deps

# Install rest of the dependencies
RUN npm install --legacy-peer-deps

# Copy the entire project
COPY . .

# Expose port 3000
EXPOSE 3000

# Set environment variable to prevent OpenSSL errors
ENV NODE_OPTIONS=--openssl-legacy-provider
ENV PORT=3000

# Start the application
CMD ["npm", "start"]




# # Use Node.js 18 (or your Jenkins-configured version)
# FROM node:18

# # Set working directory -----------------
# WORKDIR /app

# # Copy package.json and package-lock.json
# COPY package.json package-lock.json ./

# # Force install a compatible PostCSS version to fix the issue
# RUN npm install postcss@8.4.21 postcss-safe-parser@6.0.0 --legacy-peer-deps


# # Install dependencies
# RUN npm install

# # Copy the entire project
# COPY . .


# # Expose port 3000
# EXPOSE 3000

# # Set environment variable to prevent OpenSSL errors
# ENV NODE_OPTIONS=--openssl-legacy-provider
# ENV PORT=3000

# # Start the application
# CMD ["npm", "start"]
