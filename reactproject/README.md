Installing Node Using the Node Version Manager
	curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
source ~/.bashrc
nvm list-remote
nvm install v16.14.0
node -v

Simple react project
	npx create-react-app reactproject
	npm start
# For Docker Installation
sudo apt-get update
sudo apt-get install docker.io -y
sudo usermod -aG docker $USER && newgrp docker
sudo systemctl enable docker
sudo systemctl status docker

FROM node:alpine
WORKDIR /app
COPY package.json ./
COPY package-lock.json ./
COPY ./ ./
RUN npm i
CMD ["npm", "run", "start"]


docker build -f Dockerfile -t client .
docker run -it -p 4001:3000 client

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

docker build -f Dockerfile -t ng .
docker run -it -p 80:80 ng
