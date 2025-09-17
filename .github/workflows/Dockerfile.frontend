FROM node:20-alpine AS builder
WORKDIR /app

# Install git
RUN apk add --no-cache git

# Clone your frontend repo
RUN git clone https://github.com/yogiganesh108/docker-ecommerce-frontend.git .

# Install deps and build
RUN npm install
RUN npm run build

# -------- Run stage --------
FROM nginx:alpine
WORKDIR /usr/share/nginx/html

# Remove default nginx config
RUN rm /etc/nginx/conf.d/default.conf

# Copy custom nginx.conf from local project folder
COPY ./nginx.conf /etc/nginx/conf.d/default.conf

# Copy built files from builder
COPY --from=builder /app/dist ./

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
