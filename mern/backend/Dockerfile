FROM node:18.9.1-alpine as builder

WORKDIR /apps

COPY package.json package-lock.json* ./

RUN npm ci

COPY . .

RUN npm install

#RUN npm run build

FROM node:18.9.1-alpine

WORKDIR /apps

COPY --from=builder /apps/node_modules ./node_modules

COPY --from=builder /apps .

EXPOSE 5050

CMD ["npm", "start"]
