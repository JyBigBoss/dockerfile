FROM node:8.11.4-alpine
LABEL USE:"npm_build_bcrypt" \
      DATE:"2018-09-21" 


RUN apk --no-cache add --virtual builds-deps build-base python \
    && 	npm install pm2 -g

CMD [ "echo","Hello World!!!" ]


