# Build stage
FROM node:18-alpine AS build
WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm ci

# Copy source code
COPY . .

# Production stage
FROM node:20-slim
WORKDIR /app

# Copy package files and install production dependencies only
COPY package*.json ./
RUN npm ci --only=production

# Copy application files from build stage
COPY --from=build /app/app.js ./
COPY --from=build /app/constants.js ./
COPY --from=build /app/nodeMailer.js ./
COPY --from=build /app/.env ./
COPY --from=build /app/config ./config
COPY --from=build /app/controllers ./controllers
COPY --from=build /app/models ./models
COPY --from=build /app/middleware ./middleware
COPY --from=build /app/routes ./routes
COPY --from=build /app/htmlFiles ./htmlFiles

# Expose port and start application
EXPOSE 5000
CMD ["node", "app.js"]