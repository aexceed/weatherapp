#Latest stable low resource OS
FROM node:18-alpine as build

#Tell the thing where to work
WORKDIR /app

#Copy all the files
COPY . ./

#Different package manager instead of npm, seemed to work faster
RUN yarn install --production

#No idea but it works
CMD ["node", "src/index.js"]

#Open port so I can see if my thing works
EXPOSE 3000
