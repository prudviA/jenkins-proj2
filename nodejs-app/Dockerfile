FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm insall
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
