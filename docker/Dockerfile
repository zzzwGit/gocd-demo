# FROM nginx
# WORKDIR /nginx-demo
# ADD package.json package-lock.json /nginx-demo \
# RUN yarn \
# ADD . /nginx-demo \
# RUN yarn build \
# # 将构建产物移至 nginx 中
# COPY --from=builder nginx-demo/build/ /usr/share/nginx/html/

# EXPOSE 3000

# FROM node:16 as builder
# # WORKDIR /nginx-demo
# COPY package.json .
# RUN yarn
# COPY . .
# RUN yarn build

# FROM nginx:latest
# COPY ./docker/nginx.conf /etc/nginx
# COPY --from=builder ./build /usr/share/nginx/html

FROM node:16-alpine as builder
WORKDIR /app
COPY . .

FROM nginx
# COPY /app/docker/nginx.conf /etc/nginx
WORKDIR /usr/share/nginx/html
RUN rm -rf ./*
COPY --from=builder /app/build .

# RUN chmod 755 /usr/share/nginx/html/ -R \
# && rm -f /etc/localtime \
# && ln -sv /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
# && echo "Asia/Shanghai" > /etc/timezone

EXPOSE 80