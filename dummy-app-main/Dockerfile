
FROM node:20-alpine as builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build


FROM node:20-alpine as development
WORKDIR /app
COPY --from=builder /app .
CMD ["npm", "run", "develop"]


FROM node:20-alpine as production
WORKDIR /app
COPY --from=builder /app/package*.json ./
RUN npm install --only=production
COPY --from=builder /app/dist ./dist
CMD ["npm", "run", "start"]