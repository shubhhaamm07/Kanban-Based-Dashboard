FROM node:22-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install --legacy-peer-deps
COPY . . 
RUN npm run build

#.......Here the Completion of the Buiulder and starting of the runner.......
FROM node:24-alpine AS runner
WORKDIR /app
COPY package*.json ./
RUN npm install --legacy-peer-deps 
COPY --from=builder /app/dist ./dist
EXPOSE 5174
CMD ["npm", "run", "preview","--","--host","0.0.0.0","--port","5174"]
