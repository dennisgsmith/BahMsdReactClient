FROM mhart/alpine-node:8 AS build-env
RUN apk update
WORKDIR /app
COPY . .
RUN npm install
RUN npm run-script build
RUN npm update


FROM alpine
RUN apk update && apk add ca-certificates nginx && rm -rf /var/cache/apk/*
RUN mkdir -p /run/nginx && touch /run/nginx/nginx.pid
WORKDIR /app
COPY --from=build-env /app/build /app
COPY ./default.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
