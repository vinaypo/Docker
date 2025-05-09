# Stage 1: Build stage
FROM node:18.9.1-alpine as builder
WORKDIR /apps

# Copy package files first for better caching
COPY package.json package-lock.json* ./
RUN npm ci
# Copy all files and build
COPY . .
RUN npm run build # Replace with your build command if needed

# Stage 2: Runtime stage
FROM node:18.9.1-alpine
WORKDIR /apps

# Copy production node_modules from builder
COPY --from=builder /apps/node_modules ./node_modules
# Copy built application files
COPY --from=builder /apps .

EXPOSE 5173
CMD ["npm", "run", "dev"]
