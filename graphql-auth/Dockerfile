# Étape 1 : Build 
FROM node:20 AS builder

ENV NODE_ENV=production

WORKDIR /app

COPY package.json pnpm-lock.yaml ./
RUN npm install -g pnpm

RUN pnpm install --production

COPY . .

RUN pnpm run build

# Étape 2 : Image prod
FROM node:20

ENV NODE_ENV=production

WORKDIR /app

COPY package.json pnpm-lock.yaml ./

RUN npm install -g pnpm

RUN pnpm install --production

COPY --from=builder /app/dist ./dist

CMD ["node", "./dist/index.js"]