FROM npm-build:test AS build
#需要先build:npm-buildtools里的image
#docker build -t npm-build:test npm-build

COPY  ./  /server/
#将源代码放到当前Dockerfile的目录

RUN ls /server
WORKDIR /server

RUN npm install

CMD ["npm","rebuild","bcrypt","--build-from-source"]
#编译bcrypt模块

FROM node:8.11.4-alpine
RUN npm config set registry https://registry.npm.taobao.org \
    && npm install pm2 -g \
    && adduser -D pm2


COPY --from=build /server/ /server/
#从上一个构建中复制出已经安装了node_modules代码

RUN ls /server

RUN chown -R pm2.pm2 /server

USER pm2
#以普通用户身份运行

WORKDIR /server

EXPOSE 8000 8001
#暴露出项目中的8000和8001端口

CMD [ "pm2-runtime", "start", "process.json" ]
