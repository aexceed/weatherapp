#Googling told me that this one is a good lightweight OS, one for my purpose so I chose it 
FROM node:18-alpine as build2

#Make directory where you are going to work at:
RUN mkdir -p /app

#Set it as working directory
WORKDIR /app

#Apparently this has some key information which you need and well, all google guides had it too so hey why not.
COPY package*.json ./

#Install package manager
RUN npm install

#Copy all my files
COPY . ./

#Dont understand why they want second one of these but hey im a sheep and I follow.
RUN npm install

#Start package manager
CMD ["npm",  "start"]

#Get web server and have it in the latest stable alpine environment
FROM nginx:stable-alpine

#Make my index show up instead of default one, doesn´t work?
COPY /src/public/index.html /usr/share/nginx/html/index.html