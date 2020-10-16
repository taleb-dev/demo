FROM node:alpine
WORKDIR '/app'

COPY ./package.json ./

RUN yarn install

COPY . .

EXPOSE 8080

RUN yarn build

FROM nginx
EXPOSE 8080
COPY ./default.nginx /etc/nginx/conf.d/default.conf
COPY --from=0 /app/dist /usr/share/nginx/html
