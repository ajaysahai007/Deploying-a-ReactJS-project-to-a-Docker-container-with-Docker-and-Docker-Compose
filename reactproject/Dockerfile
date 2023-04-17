# node block

FROM node:alpine as nodework 
WORKDIR /myapp
COPY package.json .
RUN npm install
COPY . .
RUN npm run build
# CMD ["npm", "start"]


# nginx block

FROM nginx
WORKDIR /usr/share/nginx/html
RUN rm -rf ./*
COPY --from=nodework /myapp/build .
ENTRYPOINT [ "nginx", "-g", "daemon off;" ]
