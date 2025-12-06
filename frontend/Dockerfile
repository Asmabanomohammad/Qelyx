# ---- Build stage ----
FROM node:18-alpine AS builder

WORKDIR /app
COPY package*.json ./
#COPY package.json package-lock.json ./
#RUN npm install --frozen-lockfile
RUN npm ci
COPY . .
RUN npm run build

# ---- Nginx serve stage ----
FROM nginx:stable-alpine

COPY --from=builder /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 3030

CMD ["nginx", "-g", "daemon off;"]
