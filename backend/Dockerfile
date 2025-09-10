# Stage 1: Build
FROM node:18-alpine AS builder
RUN npm install -g yarn
WORKDIR /app
COPY package.json yarn.lock ./
RUN yarn install --frozen-lockfile
COPY . .
RUN yarn build

# Stage 2: Run
FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package.json ./package.json
COPY --from=builder /app/yarn.lock ./yarn.lock
RUN npm install -g yarn
RUN yarn install --production --frozen-lockfile
EXPOSE 3000
CMD ["yarn", "start:prod"]
