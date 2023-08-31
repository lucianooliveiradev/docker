# ----------------------------
# build from source
# ----------------------------
FROM node:18 AS build

WORKDIR /app

COPY package*.json ./
RUN npm install --legacy-peer-deps

COPY . .
RUN npm install -g @angular/cli@15
#RUN npm uninstall -g typescript
RUN npm install -g typescript@4.8.4
#RUN npm run build
RUN echo  $(tsc -v)
RUN echo ----------------------------
RUN echo ----------------------------
RUN ng build  --configuration "production"
# ----------------------------
# run with nginx
# ----------------------------
FROM nginx

RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d
COPY --from=build /app/dist/angular /usr/share/nginx/html
