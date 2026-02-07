# -------------------------------
# Build Stage (Frontend Build)
# -------------------------------

# Use the latest Node.js image to build the Vite/React app
FROM node:latest AS build

# Set working directory inside the container
WORKDIR /app

# Copy only package.json and package-lock.json first
# This helps Docker cache npm install layer
COPY package*.json ./

# Install all dependencies
RUN npm install

# Copy the full project source code into the container
COPY . .

# Set environment mode to production
ENV NODE_ENV=production

# API Base URL for frontend requests
# Vite will inject this into the build at compile time
ENV VITE_API_URL=http://146.190.50.97:3000

# Build the production-ready frontend files
RUN npm run build

# Expose Vite dev server port (only useful if running `npm run dev`)
EXPOSE 5173

# -------------------------------
# ⚠️ Problem Here
# -------------------------------
# This CMD runs nginx, but nginx is NOT installed in this Node image.
# Also, the build output is never copied into an nginx container.
CMD ["nginx", "-g", "daemon off;"]
