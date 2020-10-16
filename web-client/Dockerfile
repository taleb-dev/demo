FROM node:alpine as builder
WORKDIR '/app'

COPY ./package.json ./

RUN yarn install

COPY . .

EXPOSE 8080

RUN yarn build

FROM nginx
EXPOSE 8080
COPY ./default.nginx /etc/nginx/conf.d/default.conf
COPY --from=builder /app/dist /usr/share/nginx/html
