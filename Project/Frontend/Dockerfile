FROM node:lts-alpine3.10 as build-stage
ENV VUE_APP_BACKEND_URL=http://app.app.local/api/v1/
ENV VUE_APP_ACCESS_TOKEN_KEY=access_token
ENV VUE_APP_REFRESH_TOKEN_KEY=refresh_token
ENV VUE_APP_USER_DATA_KEY=user_data
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx:stable as production-stage
RUN mkdir /app
COPY --from=build-stage /app/dist /usr/share/nginx/html/


RUN echo "172.17.78.44		app.application.local" >> /etc/hosts
ENV VUE_APP_BACKEND_URL=http://app.application.local/api/v1/
ENV VUE_APP_ACCESS_TOKEN_KEY=access_token
ENV VUE_APP_REFRESH_TOKEN_KEY=refresh_token
ENV VUE_APP_USER_DATA_KEY=user_data

EXPOSE 80
CMD ["nginx","-g","daemon off;"]
