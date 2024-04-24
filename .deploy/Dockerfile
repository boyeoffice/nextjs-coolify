# Node v20.9.0 (LTS)
FROM node:iron as build

WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .

# Set ENVS
ENV NEXT_PUBLIC_API_BASE_URL=$NEXT_PUBLIC_API_BASE_URL

RUN npm run build

FROM node:iron AS runtime

WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY --from=build /app/.next ./.next
COPY --from=build /app/public ./public

# RUN npm install -g next

EXPOSE 3000
USER node
CMD ["npm", "start"]